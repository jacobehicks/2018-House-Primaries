*This code relies on the glue package. It assumes a list of FEC candidate IDs have been imported into a list entitled 'finalfec'.*

````

for (i in 1:length(finalfec) {
    
        tryCatch({
            print(glue("{i} - {finalfec[i]}"))
            testspending <- ""
            testspending <- try(fromJSON(glue("https://api.open.fec.gov/v1/candidate/{finalfec[i]}/committees/?api_key=8Fc9mRg4PrdIM92sx5RgX4To3tpz9bpITvg73LdI&per_page=1&committee_type=H&page=1&year=2018&sort=first_file_date&designation=P&designation=A")))
            testresults <- ""
            testresults <- testspending$results
            finaljson <- ""
            finaljson <- try(fromJSON(glue("https://api.open.fec.gov/v1/committee/{testresults$committee_id}/filings/?api_key=8Fc9mRg4PrdIM92sx5RgX4To3tpz9bpITvg73LdI&per_page=1&report_type=12P&page=1&most_recent=true&sort=-receipt_date&form_type=F3")))
            finalspending[i] <- "0"
            testresults <- ""
            testresults <- finaljson$results
            finalspending[i] <- testresults$total_disbursements
        }, error=function(e) {finalspending[i] <<- "9999999999"} )
    
}

````
