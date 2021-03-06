## Omnize Agent SDK V1
#### Authenticate user
Make HTTP request:

    POST https://services.omnize.com.br/authentication/login

With body:

    {
      "username": "test@example.org",
      "password": "password12345"
    }

Response:

    {
      "status": "200",
      "token": "......."
    }

## Getting start
#### Import SDK:

    <script src="https://omnizeagentsdk.omnize.com.br/sdk.min.js" type="text/javascript"></script>

####  Instantiate sdk passing agent token:

    const sdk = new OmnizeAgentSDK(token)

## Handlers
#### Register agent success (Online):

    sdk.on('registered', () => {})

#### Register agent failed:

    sdk.on('unauthorized', () => {})

#### Unregister agent success (Offline):

    sdk.on('unregistered', () => {})

#### New message from customer:

    sdk.on('newMessage', ({createdAt, content, interactionHash, contentType, messageId, url}) => {})

#### Agent message received on server:

    sdk.on('receivedMessage', ({messageId, interactionHash, tempId}) => {})

#### Agent message delivered to customer:

    sdk.on('deliveredMessage', ({messageId, interactionHash}) => {})

#### Customer typing:

    sdk.on('typing', (interactionHash) => {})

#### Accepted interaction:

    sdk.on('acceptedInteraction', (interactionHash) => {})

#### Customer cleared input:

    sdk.on('cleared', (interactionHash) => {})

#### Customer finished interaction:

    sdk.on('finishedInteraction', (interactionHash, reason) => {})

#### Cancel interaction to agent (Stop ringing):

    sdk.on('canceled', (interactionHash) => {})

#### Interaction was transferred successfully:

    sdk.on('transferred', (interactionHash) => {})

#### Interaction wasn't transferred:

    sdk.on('transferFailed', (interactionHash, reason = '') => {})

#### Email response sent by agent was delivered:

    sdk.on('mailDelivered', ({messageId, interactionHash, tempId}) => {})

#### Email response sent by agent fail:

    sdk.on('mailFailed', ({messageId, interactionHash, tempId}) => {})

#### New interaction received:

    sdk.on('newInteraction', ({interactionHash, id, customer, department.id, interactionType, externalHistory, currentState, createdAt}) => {})

#### Interaction update:

    sdk.on('updateInteraction', (interaction) => {})

#### When agent register in another session:

    sdk.on('kill', () => {})


## Methods
#### Connect agent to server:

    sdk.connect()

#### Register agent (Online):

    sdk.register()

#### Unregister agent (Offline):

    sdk.unregister()

#### Accept new interaction (Answer), wait for acceptedInteraction to confirm:

    sdk.acceptInteraction(interactionHash)

#### Send agent typing to customer:

    sdk.typing(interactionHash)

#### Send agent cleared to customer:

    sdk.cleared(interactionHash)

#### Send message to customer:

    tempId = sdk.newMessage(content, interactionHash, contentType)

#### Send email message to customer:

    tempId = sdk.sendMailMessage({content, interactionHash, attachments, cc, subject})

#### Transfer interaction to agent:

    sdk.transferToAgent(toAgentId, toDepartmentId, interactionHash)

#### Transfer interaction to department:

    sdk.transferToDepartment(toDepartmentId, interactionHash)

#### Send finish interaction:

    sdk.finishInteraction(interactionHash)

#### Transfer phone interaction to agent:

    sdk.transferPhoneToAgent(interactionHash)

## API methods

#### Get interaction info:

        sdk.getInteractionInfo(interactionHash, callback);

- Response

        {
            "status": 200,
            "success": true,
            "data": {
                "parsed_messages": [{"type", "id", "content"}],
                "customer": {"customerKey", "id", "historyCount", "firstContact", "fields"},
                "info": {},
                "tags": [{"id", "name", "state", "dateCreation", "baseColor", "agent": {"name", "photo"}, "count"}],
                "note": ""
            }
        }

#### Get history interaction info:

        sdk.getHistoryInteractionInfo(interactionHash, callback);

- Response

        {
            "status": 200,
            "success": true,
            "data": {
                "parsed_messages": [{"type", "id", "content"}],
                "customer": {"customerKey", "id", "historyCount", "firstContact", "fields"},
                "info": {},
                "tags": [{"id", "name", "state", "dateCreation", "baseColor", "agent": {"name", "photo"}, "count"}],
                "note": ""
            }
        }

#### Get departments/agents list to transfer interaction:

        sdk.getTransferList(callback);

- Response

        {
            message: "Success",
            status: 200,
            result: {
                agents: [...],
                departments: [...]
            }
        }

#### Get tags:

        sdk.getTags(callback);

- Response

        {
            status: 200,
            tags: [...],
            total: {...}
        }

#### Update tags
Send array with tag ids:

        sdk.updateTags(interactionHash, tagIds, callback);

- Response

        {
            "interaction": {...},
            "status": 200,
            "success": true
        }

#### Update note

        sdk.updateNote(interactionHash, note, callback);

- Response

        {
            "interaction": {...},
            "status": 200,
            "success": true
        }

#### Get/Search shotcuts:

        sdk.getShortcuts(search, callback);

- Response

        {
            status: 200,
            shortcuts: [...]
        }

#### Get/search customers:

        sdk.getCustomers(limit, page, search, callback);

- Response

        {
            status: 200,
            count: 20,
            customers: [{ "id", "historyCount", "firstContact", "customerKey", "fields" }]
        }

#### Get customer history:

        sdk.getCustomerHistory(customerKey, limit, page, search, callback);

- Response

        {
            "result": {
                "interactions": [{ "startTime", "department", "id", "hash", "lastMessage", "type", "tags", "origin", "customerMediaId"}]
            },
            "status": 200
        }

#### Update customer:
- Send fields formated like:

        fields: { field.name: field.value, field.name: field.value ... }

        ie.: fields: { "main_identifier": "Client Tester", "channel_email": "client@tester.com" ... }

- Method

        sdk.updateCustomer(customerKey, fields, callback);

- Response

        {
            "customer": {...},
            "status": 200
        }

#### Change customer:

        sdk.changeCustomer(interactionHash, customerId, callback);

- Response

        {
            "customer": {...},
            "status": 200
        }

#### Merge customers:

        sdk.mergeCustomers(newCustomerKey, oldCustomerKey, fields, callback);

- Response

        {
            "customer": {...},
            "status": 200,
            "success": true
        }

#### Get form fields:

        sdk.getFormFields(callback);

- Response

        {
            "status": 200,
            "formFields": [{...}]
        }

#### Get queue interactions:

        sdk.getQueue(limit, page, callback)

- Response:

        {
            "interactions": [...],
            "status": 200,
            "success": true
        }

#### Get inbox interactions:

        sdk.getInbox(limit, page, search, callback)

- Response:

        {
            "interactions": [...],
            "status": 200,
            "success": true
        }


#### Get interactions count:

        sdk.getCount(callback)

- Response:

        {
            "inbox": 2,
            "queue": 2,
            "status": 200,
            "success": true,
            "total": 4
        }

#### Get online agents:

        sdk.getOnlineAgents(callback)

- Response:

        {
            "agents": [online_agents],
            "success": true,
            "total": 2
        }

#### Get agent history:

        sdk.getHistory(limit, page, search, callback)

- Response:

        {
            "interactions": [...],
            "status": 200,
            "success": true
        }
        
#### Send chat email:

        sdk.sendChatEmail(toEmail, callback)

- Response:

        {
            "status": 200,
            "success": true
        }


