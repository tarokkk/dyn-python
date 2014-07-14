# Dyn Python SDK


NOTE: This SDK is brand new - we welcome your feedback!
Please reach out via pull request or GitHub issue.

Install this package via:

    pip install dyn-python

Making DNS Updates as easy as:

    from dyn.traffic import DynTraffic

    # create a new instance of the API client
    dyn = DynTraffic('customername', 'username', 'password').with_zone('example.com')

    # establish an API connection
    dyn.session.create()


    # create an A record
    dyn.record.create('A', 'www.example.com.', {'address':'1.2.3.4'})

    # create a CNAME record
    dyn.record.create('CNAME', 'www2.example.com.', {'cname':'www.example.com'})


    # delete one A record
    dyn.record.delete('A', 'www.example.com', <record_id>)

    # delete all A record
    dyn.record.delete('A', 'www.example.com')

    # delete a CNAME record
    dyn.record.delete('CNAME', 'www2.example.com')


    # publish changes
    dyn.zone.publish()

    #Get all records from the zone
    dyn.zone.list()

    #Get all records from the node
    dyn.zone.list('www.example.com')


    # log out to finish session
    dyn.session.destroy()

Working with Messaging is as easy as:

    import sys
    from dyn.messaging import DynMessaging
    import json
    
    def show(message, result):
        sys.stderr.write(message + ": " + json.dumps(result) + '\n\n')
    
    client = DynMessaging('yourapikey')
    client._client.verbose = False
    
    # accounts (create, list, list_xheaders, update, update_headers, destroy)
    show("ACCOUNTS LIST", client.accounts.list())
    show("ACCOUNTS CREATE", client.accounts.create("some@address.com", "secretword", "some company", "1234567890", "123 main st", "big city", "MA", "12345", "USA", "east", "bounces.com", "spam.com", "unsubscribe.com", "trackopens.com", "tracelinks.com", "trackunsubscribes.com", "generatenewapikey.com"))
    show("ACCOUNTS UPDATE", client.accounts.update("some@address.com", "secretword", "some company", "1234567890", "123 main st", "big city", "MA", "12345", "USA", "east", "bounces.com", "spam.com", "unsubscribe.com", "trackopens.com", "tracelinks.com", "trackunsubscribes.com", "generatenewapikey.com"))
    show("ACCOUNTS DESTROY", client.accounts.destroy("some@address.com"))
    show("XHEADERS LIST", client.accounts.list_xheaders())
    show("XHEADERS UPDATE", client.accounts.update_xheaders('X-MyExample1','X-AnotherExample2','X-Interesting3','X-Important4'))
    
    # senders (list, details, status, create, update, dkim, destroy)
    show("SENDERS LIST", client.senders.list())
    show("SENDERS DETAILS", client.senders.details("some@address.com"))
    show("SENDERS STATUS", client.senders.status("some@address.com"))
    show("SENDERS CREATE", client.senders.create("some@address.com"))
    show("SENDERS UPDATE", client.senders.update("some@address.com"))
    show("SENDERS DKIM", client.senders.dkim("some@address.com", "123dkim"))
    show("SENDERS DESTROY", client.senders.destroy("some@address.com"))
    
    # recipients (status, activate)
    show("RECIPIENTS STATUS", client.recipients.status("some@address.com"))
    show("RECIPIENTS ACTIVATE", client.recipients.activate("some@address.com"))
    
    # suppressions (list, count, create, activate)
    show("SUPPRESSIONS LIST", client.suppressions.list())
    show("SUPPRESSIONS COUNT", client.suppressions.count())
    show("SUPPRESSIONS CREATE", client.suppressions.create("something@address.com"))
    show("SUPPRESSIONS ACTIVATE", client.suppressions.activate("something@address.com"))
    
    # send mail (send)
    show("SEND MAIL", client.send_mail.send("from@somedomain.com", "to@someotherdomain.com", 'hello', 'from python api', "<html><body>'hi from python api'</body></html>", "somecc@address.com", "somereply@address.com"))

    # report - delivery (list, count)
    show("DELIVERY REPORT", client.delivery.list('2014-01-01','2014-08-01'))
    show("DELIVERY COUNTS", client.delivery.count('2014-01-01','2014-08-01'))


# Examples

For more comprehensive examples, check out the "examples" folder.

# API Endpoints Supported

* Traffic - Session API: create/destroy
* Traffic - Record API: AAAA A CNAME DNSKEY DS KEY LOC MX NS PTR RP SOA SRV TXT
* Traffic - Zone API: list/get/publish/freeze/thaw
* Traffic - Http Redirect API: create/update/list/destroy
* Messaging - All Endpoints Supported

# Known Issues

* None yet

# License

BSD 3-clause
