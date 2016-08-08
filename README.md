# msgqueue



global class DeleteMsgQueueRecordsBatch implements Database.Batchable<sObject>{
    global String Query;
    

    global Database.QueryLocator start(Database.BatchableContext BC){
      query = 'select id from MessageQueue__c WHERE CreatedDate < LAST_N_MONTHS:12';
            
       if (Test.isRunningTest()) {
            query += '  limit 5';
        }

        return Database.getQueryLocator(query);
    }

    global void execute(Database.BatchableContext BC,List<MessageQueue__c> scope){

        delete scope;
    }

    global void finish(Database.BatchableContext BC){}
}
