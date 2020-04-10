`

*This code relies on the rtweet, and glue packages. It assumes a list of twitter usernames have been imported into a list entitled 'users'.*

for (i in 1:length(users)) {
    if (exists(paste(users[i]))) print(glue("User {users[i]} exists - skipping."))
    if (exists(paste(users[i]))) next
    rl <- rate_limit("get_friends")
    total <- length(users)
    print(glue("Downloading {i} of {total}."))
    if (rl$remaining > 0) {
        
        if (!exists(paste(users[i]))) {
            assign(paste(users[i]), get_friends(users[i],n = 5000,retryonratelimit = TRUE,page = "-1",parse = TRUE,verbose = TRUE,token = NULL))
        }
        
    } else {
        wait <- rl$reset + 0.1
        print(glue("Waiting for {wait} minutes."))
        Sys.sleep(wait * 60)
    }
}

`
