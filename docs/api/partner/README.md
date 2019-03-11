## Partner Portal
To get partner token, access:

    http://partner.omnize.com

For login/password contact suporte@omnize.com

## Partner API

#### Create Agent
Make HTTP request:

    POST http://partner.omnize.com/api/v1/agents

With body:

    {
      token: 'j423j42jn3kj4n',
      profile: 'ADMIN', // 'ADMIN' or 'AGENT'
      agent: {
        email: 'test@example.com', // Email used to login
        name: 'Test Agent',
        password: 'j2hk2j3h4kj23h4kjh2k34', // Plain text signed as SHA256 hash
        text_limit: 7, // optional 
        account_id: 1111
      }
    }

Without parameter profile, will create a AGENT profile

Response, success:

    {
      status: 200,
      success: true,
      data: {
        id: 12153,
        name: "New Agent",
        password: nil,
        administrator: "NAO",
        email: "agent@example.com",
        ativo: 1,
        photo: nil,
        subscriber_id: nil,
        account_id: 3373,
        date_creation: "2017-06-20 20:24:51",
        change_date: "2017-06-20 20:24:51",
        user_creation: nil,
        user_change: nil,
        version_register: 0,
        register_mobile_id: nil,
        photo_expired_date: nil,
        bucket_conf: nil
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update Agent
Make a HTTP request:

    PUT http://partner.omnize.com/api/v1/agents/:id

With body:

    {
      token: 'j423j42jn3kj4n',
      agent: {
        email: 'update@example.com',
        name: 'New Name',
        text_limit: 7, // optional 
        password: 'j2hk2j3h4kj23h4kjh2k34' // Plain text signed as SHA256 hash
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "E-mail can be blank"
    }

#### Update Agent Profile
Make a HTTP request:

    PUT http://partner.omnize.com/api/v1/agents/:id/profile

With body:

    {
      token: 'j423j42jn3kj4n',
      profile: 'AGENT'
    }

Response, success:

    {
      status: 200,
      success: true
    }

#### Retrieve all agents
Make HTTP request:

    GET http://partner.omnize.com/api/v1/agents?token=hj4h2k3h4k23&account_id=1

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }


#### Create Account
Make HTTP request:

    POST http://partner.omnize.com/api/v1/accounts

With body:

    {
      token: 'hj4h2k3h4k23',
      license_quantity: 10,
      password: 'j2hk2j3h4kj23h4kjh2k34', (Optional) // SHA256
      account: {
        email: 'test@example.com',
        main_contact: 'Account Owner Namer',
        telefone: '(11) 9345-0987',
        url: 'testwebpage.com.br'
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: {
        id: 4931,
        name: nil,
        razao_social: nil,
        inscricao_estadual: nil,
        cpfcnpj: nil,
        endereco: nil,
        bairro: nil,
        cidade: nil,
        estado: nil,
        telefone: "(11) 98877-6655",
        telefone1: nil,
        email: "test@example.org",
        main_contact: "Test Account",
        iugu_id: nil,
        validate_hash: true,
        subscriber_id: nil,
        domain_id: 4926,
        ativo: 1,
        version_register: 0,
        user_creation: nil,
        date_creation: "2017-06-02 19:24:00",
        user_change: nil,
        change_date: "2017-06-02 19:24:00",
        cep: nil,
        user_last_access: nil,
        date_last_access: nil,
        region_id: 36,
        segment_id: 1,
        url: "www.test.com",
        whatsapp: nil,
        token: nil,
        partner_id: 1,
        facelift: true
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }
    
#### Update Account
Make HTTP request:

    PUT http://partner.omnize.com/api/v1/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      account: {
        email: 'test@example.com',
        main_contact: 'Account Owner Namer',
        telefone: '(11) 9345-0987',
        url: 'testwebpage.com.br',
        ativo: 1
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: {
        id: 4931,
        name: nil,
        razao_social: nil,
        inscricao_estadual: nil,
        cpfcnpj: nil,
        endereco: nil,
        bairro: nil,
        cidade: nil,
        estado: nil,
        telefone: "(11) 98877-6655",
        telefone1: nil,
        email: "test@example.org",
        main_contact: "Test Account",
        iugu_id: nil,
        validate_hash: true,
        subscriber_id: nil,
        domain_id: 4926,
        ativo: 1,
        version_register: 0,
        user_creation: nil,
        date_creation: "2017-06-02 19:24:00",
        user_change: nil,
        change_date: "2017-06-02 19:24:00",
        cep: nil,
        user_last_access: nil,
        date_last_access: nil,
        region_id: 36,
        segment_id: 1,
        url: "www.test.com",
        whatsapp: nil,
        token: nil,
        partner_id: 1,
        facelift: true
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }
    

#### Inactive Account
Make HTTP request:

    PUT http://partner.omnize.com/api/v1/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      account: {
        ativo: 0
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Active Account
Make HTTP request:

    PUT http://partner.omnize.com/api/v1/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      account: {
        ativo: 1
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }


#### Delete Account
Make HTTP request:

    DELETE http://partner.omnize.com/api/v1/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23'
    }

Response, success:

    {
      status: 200,
      success: true,
      message: "Account deleted successfully"
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update account licenses
Make HTTP request:

    PUT http://partner.omnize.com/api/v1/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      license_quantity: 5
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update account licenses code
Make HTTP request:

    PUT http://partner.omnize.com/api/v1/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      license_code: 'PARTNER_X'
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Widget
Widget-code, set proper account_id at 'wOmz.init({id:#{id}})':

    <!-- Início do script Omnize -->
      <script>
        document.addEventListener('DOMContentLoaded',function(){
          var JSLink=location.protocol+'//widget.omnize.com',JSElement=document.createElement('script');
          JSElement.async=!0;
          JSElement.src=JSLink;
          JSElement.onload=OnceLoaded;
          document.getElementsByTagName('body')[0].appendChild(JSElement);
          function OnceLoaded(){
            wOmz.init({id:#{id}});
          }
        },false);
      </script>
    <!-- Fim do script Omnize -->


#### Url login
Make a http request to generate auth_token:

    POST https://ca1vsqktff.execute-api.us-east-1.amazonaws.com/prod/authentication

Body:

    {
      "action": "loginPartner",
      "username":"user@example.org", // Agent email
      "token":"B4cPxMMVteyoqCk6UUsK" // Partner token
    }

Response:

    {
      "message": "",
      "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVaRp5D0e3",
      "status": 200
    }

Link to login, with returned token:

    https://login.omnize.com.br?token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVaRp5D0e3


## Manage Departments
#### Create
Make HTTP request:

    POST http://partner.omnize.com/api/v1/departments

With body:

    {
      token: 'hj4h2k3h4k23',
      department: {
        account_id: 1,
        name: "New Department",
        description: "A new created department",
        ativo: 1,
        channels: ["chat","video","audio"]
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [createdObject]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update
Make HTTP request:

    PUT http://partner.omnize.com/api/v1/departments/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      department: {
        name: "New Department Name",
        description: "New department description",
        ativo: 0
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [updatedObject]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve all
Make HTTP request:

    GET http://partner.omnize.com/api/v1/departments?token=hj4h2k3h4k23&account_id=1

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfDepartments]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve all channels
Make HTTP request:

    GET http://partner.omnize.com/api/v1/departments/:id/channels?token=hj4h2k3h4k23

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfChannels]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve all agents on a department
Make HTTP request:

    GET http://partner.omnize.com/api/v1/departments/:id/agents?token=hj4h2k3h4k23

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Add agents
Make HTTP request:

    POST http://partner.omnize.com/api/v1/departments/:id/add_agents

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      agents: ["123","456"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Remove agents
Make HTTP request:

    POST http://partner.omnize.com/api/v1/departments/:id/remove_agents

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      agents: ["123","456"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Add channels
Make HTTP request:

    POST http://partner.omnize.com/api/v1/departments/:id/add_channels

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      channels: ["audio"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfChannels]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Remove channels
Make HTTP request:

    POST http://partner.omnize.com/api/v1/departments/:id/remove_channels

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      channels: ["video"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfChannels]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

