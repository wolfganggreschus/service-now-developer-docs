When you’re building a ServiceNow app with the Pro Code (SDK + VS Code) approach, the “right” UI path really depends on what kind of UI you’re building and how modern / scalable you want it to be. The platform currently has three main UI approaches, and they’re not equal.

🧭 The short answer (best practice)
👉 Use UI Builder + Now Experience (UI Framework) for almost all new apps
👉 Use SDK locally for logic, components, and app structure
👉 Avoid UI Pages unless you really need legacy behavior

🧱 Your main UI options (explained)
1. 🚀 Now Experience + UI Builder (Recommended)
This is the modern ServiceNow frontend stack.

What it is
Component-based UI (similar to React)
Built using Now Experience Framework
Assembled visually in UI Builder
Can integrate custom components built locally via SDK
Why it’s best
Official future direction of ServiceNow
Clean separation: UI vs logic vs data
Reusable components
Works well with App Engine Studio + Pro Code hybrid
Supports Workspaces, Portals, internal tools
How it fits your workflow
Build custom components locally with SDK (VS Code)
Deploy them
Use them inside UI Builder pages
👉 This is the “Pro Code + Low Code hybrid” sweet spot

2. 🧩 Service Portal (AngularJS) (Legacy-ish)
What it is
Widget-based UI (AngularJS)
Still widely used
When to use
Maintaining existing portals
Customer Service portals already built on it
Why not for new apps
AngularJS is deprecated
Not future-proof
Limited compared to Now Experience
3. ⚠️ UI Pages (Jelly + HTML/JS) (Avoid for new work)
What it is
Old-school rendering using Jelly
Full manual control of HTML/JS
Downsides
Hard to maintain
Not aligned with modern ServiceNow UX
No component model
Poor scalability
👉 Only use if:

You need something very low-level
Or you're working with legacy features
🧠 Best Practice Architecture (what pros do)
✅ Recommended stack
Backend
Script Includes
REST APIs / Scripted APIs
Data model (tables)
Frontend
UI Builder (pages)
Now Experience components
Custom Web Components (built via SDK)
Local Dev (VS Code)
ServiceNow CLI / SDK
Source control (Git)
CI/CD pipeline
🛠️ Typical Pro Workflow
Develop app structure locally (SDK)
Create business logic (Script Includes, APIs)
Build custom UI components locally
Deploy to instance
Assemble UI in UI Builder
Bind data via:
Data resources
REST APIs
Client state
💡 Key Insight (this trips people up)
👉 UI Builder is NOT replacing coding — it’s orchestrating it

Think of it like:

SDK = backend + custom components
UI Builder = layout + wiring
🔥 When you SHOULD code UI locally
Use SDK + custom components when:

You need complex UI logic
Reusable UI pieces
Advanced interactions
Performance control
🚫 When NOT to over-engineer
Don’t build everything from scratch if:

UI Builder components already solve it
It’s just CRUD / forms / lists
🧭 Decision Guide
Use Case	Best Approach
New enterprise app	✅ UI Builder + Now Experience
Complex custom UI	✅ SDK + custom components + UI Builder
Simple internal tool	✅ UI Builder only
Legacy system	⚠️ Service Portal
Full control / hacky solution	❌ UI Pages
🏁 Bottom line
👉 Modern ServiceNow = UI Builder + Now Experience + SDK

If you're going “Pro Code”, the winning combo is:

Build logic + components locally, assemble UI with UI Builder




---

what do you mean with Develop app structure locally (SDK), please give me an example
Good question — this is exactly where the “Pro Code” mindset in ServiceNow starts to differ from the classic in-platform development.

When I say “develop app structure locally (SDK)”, I mean:

👉 You define and organize your entire application as code in VS Code
👉 Instead of creating everything manually in the ServiceNow UI

🧱 What “app structure” actually includes
In ServiceNow, your app isn’t just UI. It’s made of:

Data model (tables, fields)
Business logic (Script Includes, Business Rules)
APIs (Scripted REST APIs)
UI components (Now Experience components)
Config (ACLs, etc.)
With the SDK, these become files + folders in your project

📁 Example project structure (realistic)
Here’s what a typical local ServiceNow app might look like:

my-servicenow-app/
│
├── now-ui/                     # Frontend (Now Experience)
│   ├── components/
│   │   └── my-dashboard/
│   │       ├── index.js
│   │       ├── view.js
│   │       └── styles.scss
│   │
│   └── app.config.json
│
├── src/                        # Backend logic
│   ├── script-includes/
│   │   └── MyAppService.js
│   │
│   ├── business-rules/
│   │   └── updateStatus.js
│   │
│   ├── rest-api/
│   │   └── my_api.js
│
├── sys_db_object/              # Tables
│   └── x_my_app_task.json
│
├── sys_security_acl/           # Security
│   └── task_acl.json
│
├── manifest.json               # App metadata
└── package.json
🔍 What this actually replaces in the UI
Instead of doing this manually:

Creating tables in Studio
Writing Script Includes in the browser
Configuring APIs via forms
👉 You define them as files like:

🧠 Example: Script Include (local file)
// src/script-includes/MyAppService.js

var MyAppService = Class.create();
MyAppService.prototype = {
    initialize: function() {},

    getTasks: function() {
        var gr = new GlideRecord('x_my_app_task');
        gr.query();

        var results = [];
        while (gr.next()) {
            results.push({
                name: gr.getValue('name'),
                status: gr.getValue('status')
            });
        }
        return results;
    },

    type: 'MyAppService'
};
👉 This would normally be created in the ServiceNow UI
👉 Now it lives in your repo, version-controlled

🌐 Example: Scripted REST API
// src/rest-api/my_api.js

(function process(/*RESTAPIRequest*/ request, /*RESTAPIResponse*/ response) {

    var service = new MyAppService();
    var data = service.getTasks();

    response.setBody(data);

})(request, response);
⚛️ Example: UI Component (Now Experience)
// now-ui/components/my-dashboard/index.js

import {createCustomElement} from '@servicenow/ui-core';
import snabbdom from '@servicenow/ui-renderer-snabbdom';

const view = (state) => {
    return (
        <div>
            <h1>My Dashboard</h1>
            <p>Welcome to my app</p>
        </div>
    );
};

createCustomElement('x-my-dashboard', {
    renderer: {type: snabbdom},
    view
});
🔁 How this connects back to ServiceNow
After building locally, you:

Use the ServiceNow CLI / SDK
Deploy your app to your instance
It becomes:
Tables in DB
Script Includes
UI components available in UI Builder
🧭 Then UI Builder comes in
Once deployed:

Open UI Builder
Create a page
Drag your custom component (x-my-dashboard)
Bind it to data (API, state, etc.)
💡 Why this is powerful
Compared to classic development:

Classic	Pro Code (SDK)
Manual UI config	Code-driven
Hard to version	Git-friendly
Risky deployments	CI/CD ready
Hard to reuse	Modular
🔥 Mental model
Think of it like this:

SDK project = your source of truth
ServiceNow instance = runtime environment
🏁 Simple example flow
Create project locally
Add:
Table JSON
Script Include
UI component
Deploy
Use UI Builder to assemble UI