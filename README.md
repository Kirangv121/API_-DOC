# API_-DOC

#### ERPNext In-built APIs
1. Authentication APIs
2. Resource (Document) API
     The main CRUD API for any DocType.
      List documents ->   GET /api/resource/{doctype}

      Create document ->  POST /api/resource/{doctype}
                          Content-Type: application/json
                          { "customer_name": "ABC Corp", "customer_group": "Commercial" }
   
      Update document -> PUT /api/resource/{doctype}/{name}
                         { "customer_group": "SMB" }

      Delete document ->  DELETE /api/resource/{doctype}/{name}
