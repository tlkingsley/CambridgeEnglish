# CambridgeEnglish
Here is how I successfully configured the Slate Source Format to bring in scores from the Cambridge English Results Verification Service (RVS) API:
1. Create your Cambridge English RVS account: "To request a Slate account, please log in to [your institution's] [Cambridge English Results Verification Service](https://cambridge.my.site.com/s/) (RVS) account.  At the top menu bar, look for “API” and follow instructions." 
2. Refer to the [KB article](https://knowledge.technolutions.com/hc/en-us/articles/360034670112-IELTS-Results-Service-Integration) for setting up the IELTS integration in Slate; this will be _similar_ to that, but definitely not identical 
    - For the Import Remote Server URL (Step #5), use `https://apis.cambridgeassessment.org.uk/ce/v1/result-verification?startDateTime={{dtstart|date:'s'}}&endDateTime={{dtend|date:'s'}}`
    - For the HTTP Header, follow the instructions (Step #6)
    - For the Last Remote Server Fetch, this needs to be LESS THAN one year in the past
      - (Thanks to the [Postman app](https://www.postman.com/) for displaying this error that wasn't coming through into Slate: "Message Not processed: Please provide a valid Date Range. Start Date and End Date should within one year ")
      - If needed, you can hardset the start and end dates to go back further, but you can't exceed 1 year difference between the two dates
3. Create the Format Definition
   - You'll need to create your own format definition, following the basic structure in the [KB article](https://knowledge.technolutions.com/hc/en-us/articles/16558318272539#web_services)https://knowledge.technolutions.com/hc/en-us/articles/16558318272539#web_services on web services (the JSON part).
   - JSON (and XML) formats can have nested sets of data - e.g. multiple Cambridge English exams by bye same person. This format definition supports up to two tests for one person; you can modify it to support more if needed (refer the KB article above to see the syntax for nested data/arrays).
  ```
<layout type="json" node="/ListCandidateResultDetails">
  <f s="CandidateUCIId" id="CandidateUCIId" />
  <f s="CandidateName" id="CandidateName" />
  <f s="CandidateFamilyName" id="CandidateFamilyName" />
  <f s="CandidateDOB" id="CandidateDOB" />
  <f s="ReceivedDate" id="ReceivedDate" />
  <f s="ExamType" id="ExamType" />
  <f s="CandidateEmailId" id="CandidateEmailId" />
  <f s="CandidateResults[1]/Qualification" id="Qualification1" />
  <f s="CandidateResults[1]/Grade" id="Grade" />
  <f s="CandidateResults[1]/ComponentList[1]/Name" id="Qual1Comp1Name" />
  <f s="CandidateResults[1]/ComponentList[1]/Score" id="Qual1Comp1Score" />
  <f s="CandidateResults[1]/ComponentList[2]/Name" id="Qual1Comp2Name" />
  <f s="CandidateResults[1]/ComponentList[2]/Score" id="Qual1Comp2Score" />
  <f s="CandidateResults[1]/ComponentList[3]/Name" id="Qual1Comp3Name" />
  <f s="CandidateResults[1]/ComponentList[3]/Score" id="Qual1Comp3Score" />
  <f s="CandidateResults[1]/ComponentList[4]/Name" id="Qual1Comp4Name" />
  <f s="CandidateResults[1]/ComponentList[4]/Score" id="Qual1Comp4Score" />
  <f s="CandidateResults[1]/ComponentList[5]/Name" id="Qual1Comp5Name" />
  <f s="CandidateResults[1]/ComponentList[5]/Score" id="Qual1Comp5Score" />
  <f s="CandidateResults[1]/Score" id="Score1" />
  <f s="CandidateResults[1]/CefrLevel" id="CefrLevel1" />
  <f s="CandidateResults[2]/Qualification" id="Qualification1" />
  <f s="CandidateResults[2]/Grade" id="Grade" />
  <f s="CandidateResults[2]/ComponentList[1]/Name" id="Qual1Comp1Name" />
  <f s="CandidateResults[2]/ComponentList[1]/Score" id="Qual1Comp1Score" />
  <f s="CandidateResults[2]/ComponentList[2]/Name" id="Qual1Comp2Name" />
  <f s="CandidateResults[2]/ComponentList[2]/Score" id="Qual1Comp2Score" />
  <f s="CandidateResults[2]/ComponentList[3]/Name" id="Qual1Comp3Name" />
  <f s="CandidateResults[2]/ComponentList[3]/Score" id="Qual1Comp3Score" />
  <f s="CandidateResults[2]/ComponentList[4]/Name" id="Qual1Comp4Name" />
  <f s="CandidateResults[2]/ComponentList[4]/Score" id="Qual1Comp4Score" />
  <f s="CandidateResults[2]/ComponentList[5]/Name" id="Qual1Comp5Name" />
  <f s="CandidateResults[2]/ComponentList[5]/Score" id="Qual1Comp5Score" />
  <f s="CandidateResults[2]/Score" id="Score1" />
  <f s="CandidateResults[2]/Score" id="Score1" />
  <f s="CandidateResults[2]/CefrLevel" id="CefrLevel1" />
</layout>
```
4. Map values as per usual (Step #21 and #13)
