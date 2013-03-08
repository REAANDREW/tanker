EventSourcingInNode

mainRepository.prototype.save = function(domainObject, callback) {
    this.eventStore.saveEvents(domainObject.uncommittedEvents, function(){
        domainObject.markAsCommitted();
        callback();
    });
}

DomainRepository.prototype.get = function(proto, id, callback){
    this.eventStore.getEvents(id, function(events){
        var root = new proto({
            events : events
        });
        callback(root);
    });
}


Simple event sourcing library for node.js
