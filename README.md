# API_-DOC

### ERPNext In-built APIs
#### 1. Authentication APIs
#### 2. Resource (Document) API
        The main CRUD API for any DocType.
   
     For ->
      List documents ->   GET /api/resource/{doctype}

      Create document ->  POST /api/resource/{doctype}
                          Content-Type: application/json
                          { "customer_name": "ABC Corp", "customer_group": "Commercial" }
   
      Update document -> PUT /api/resource/{doctype}/{name}
                         { "customer_group": "SMB" }

      Delete document ->  DELETE /api/resource/{doctype}/{name}

#### 3. Method API -> Runs whitelisted Python functions.

         Example: login is itself a method API.

      General form:  POST /api/method/{path.to.method}
#### 4. Report APIs

      ERPNext exposes reports (Standard + Custom).
      Query/Script Report:  GET /api/method/frappe.desk.query_report.run?report_name=Receivable%20Summary&filters={"customer":"CUST-0001"}


#### 5. Search/Link APIs

    Used by link fields in forms (autocomplete).

    Search Link: GET /api/method/frappe.desk.search.search_link
    ?doctype=Customer&txt=abc&filters={}

    Get Value (field lookup): GET /api/method/frappe.client.get_value?doctype=Customer&filters={"name":"CUST-0001"}&fieldname=customer_group

#### 6. File Upload/Download API

        Upload File:  POST /api/method/upload_file
                     Content-Type: multipart/form-data
                    file=<binary> & doctype=Customer & docname=CUST-0001
 
        Download File: GET /private/files/{filename}

#### 7. DocType Schema API
        Get Meta (DocType definition) -> GET /api/method/frappe.desk.form.load.getdoctype?doctype=Sales%20Invoice

#### 8. Realtime API
    ERPNext includes WebSocket endpoints (via socket.io) for push notifications:
     e.g., frappe.publish_realtime("msgprint", {"message": "Hello"})



# Then what do you need to build?
  ### 1. AI → ERPNext Middleware API
    One custom whitelisted method,
    e.g.:POST /api/method/ai_assistant.process_command
    This API will: Accept a generic payload from  AI 
    like: {
     "action": "create",
    "doctype": "Employee",
    "fields": {
    "employee_name": "John Doe",
    "department": "Sales"
     }
    }


### 2. Optional: Custom Logic APIs

     Sometimes CRUD is not enough
     for example: “Approve leave request” → Needs a workflow action.
                  “Generate salary slip for August” → Needs a server script.
                  “Send sales order email” → Needs ERPNext’s built-in method.
    For these,  build custom whitelisted methods in ERPNext and expose them as APIs
     e.g.:POST /api/method/hrms.leave_approval.approve
          POST /api/method/accounts.salary.create_slip








