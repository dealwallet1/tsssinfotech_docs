# Manufacturing Chatbot Module Documentation

---

## 1. Overview

The **Manufacturing Chatbot Module** is a custom AI-powered solution developed for **Odoo 19 Community** to simplify manufacturing operations through conversational interactions. The chatbot is integrated with both the **Manufacturing** and **Discuss** modules, enabling users to retrieve business information, upload documents, automate business processes, and communicate with the system using natural language.

The chatbot supports multiple interaction methods, including **text input**, **voice input**, and **PDF document uploads**. It leverages the **Agno AI Agent** together with the **Groq API** to process user requests and provide intelligent responses. In addition to answering business-related queries, the chatbot automates Purchase Order creation from uploaded documents and provides quick access to related Manufacturing Orders.

By integrating AI capabilities into the Manufacturing workflow, the module reduces manual effort, improves operational efficiency, and enhances the overall user experience within Odoo.

---

## 2. Objectives

The Manufacturing Chatbot Module was implemented to:

- Provide an AI-powered assistant for Manufacturing operations.
- Enable users to interact with the system using natural language.
- Support text, voice, and PDF-based interactions.
- Retrieve business information instantly.
- Automate Purchase Order creation from uploaded documents.
- Reduce manual data entry.
- Improve productivity through intelligent business automation.
- Integrate chatbot functionality within the Odoo Discuss module.
- Enhance accessibility and user experience.

---

## 3. Features Implemented

### 3.1 Chatbot Initialization

A custom chatbot interface was developed using **OWL JavaScript** and integrated into the Odoo backend.

#### Implemented Features

- Floating chatbot widget
- OWL-based frontend interface
- Manufacturing module integration
- Agno AI Agent integration
- Interactive chatbot window

#### Workflow

```text
User Opens Odoo
       │
       ▼
Clicks Chatbot Icon
       │
       ▼
Chatbot Window Opens
       │
       ▼
Ready to Accept User Requests
```

---

### 3.2 User Interaction

The chatbot supports multiple input methods, allowing users to communicate in different ways.

#### Supported Input Methods

- Text Messages
- Voice Commands
- PDF Document Upload

#### Text Interaction

Users can directly type business-related questions into the chatbot.

Example queries include:

- Total Purchase Orders
- Total Sales Orders
- Total Manufacturing Orders
- Total Products

The chatbot processes the request and returns the appropriate response.

---

#### Voice Interaction

Voice support was implemented using the browser's Speech Recognition functionality.

#### Workflow

```text
User Clicks Microphone
        │
        ▼
Speech Recognition Starts
        │
        ▼
Voice Converted to Text
        │
        ▼
Text Sent to Chatbot
        │
        ▼
AI Generates Response
```

---

#### PDF Upload

Users can upload business documents directly through the chatbot.

Supported document types include:

- Purchase Orders
- Sales Orders
- Quotations
- Invoices

Uploaded documents are automatically processed for data extraction.

---

## 4. PDF Processing

### 4.1 PDF Upload

The chatbot allows users to upload PDF documents directly through the chatbot interface for automatic processing.

Supported document types include:

- Purchase Orders
- Sales Orders
- Quotations
- Invoices

#### Workflow

```text
User Uploads PDF
       │
       ▼
Convert PDF to Base64
       │
       ▼
RPC Request
       │
       ▼
/manufacturing_chatbot/upload_pdf
       │
       ▼
Python Controller
       │
       ▼
Document Extraction API
```

---

### 4.2 PDF Data Extraction

The uploaded PDF is processed through the document extraction service to identify and extract important business information automatically.

#### Extracted Information

- Vendor Name
- Customer Name
- Invoice Number
- Quotation Number
- Order Date
- Expiry Date
- Product Name
- Quantity
- Unit Price
- Tax
- Total Amount
- Payment Terms

Example extracted information:

```text
Quotation Number : S00001

Customer : Sai Krishna

Product : Sofa

Quantity : 1

Unit Price : 1.50

Tax : 15%
```

---

## 5. Discuss Module Integration

The Manufacturing Chatbot was integrated into the Odoo Discuss module, allowing users to interact with the chatbot without leaving the discussion environment.

Users can ask Manufacturing-related questions directly from Discuss, and the chatbot responds within the same conversation.

### Workflow

```text
User Sends Message
        │
        ▼
Discuss Channel
        │
        ▼
Manufacturing Chatbot
        │
        ▼
Python Controller
        │
        ▼
Agno AI Agent
        │
        ▼
AI Response
        │
        ▼
Reply Displayed in Discuss
```

### Benefits

- Easy access from Discuss
- Faster communication
- No need to switch modules
- Consistent chatbot experience
- Improved collaboration among users

---

## 6. Voice Recognition Support

The chatbot includes voice recognition functionality, enabling users to communicate through speech instead of typing.

Voice input is converted into text using the browser's Speech Recognition API before being processed by the chatbot.

### Workflow

```text
User Clicks Microphone
        │
        ▼
Speech Recognition Starts
        │
        ▼
Voice Converted to Text
        │
        ▼
Text Sent to Chatbot
        │
        ▼
Agno AI Agent
        │
        ▼
Chatbot Response Displayed
```

### Features

- Voice-to-text conversion
- Hands-free interaction
- Faster query submission
- Improved accessibility

---

## 7. Benefits

The Manufacturing Chatbot Module provides the following benefits:

- AI-powered assistance for Manufacturing operations.
- Faster access to Manufacturing information.
- Reduced manual effort through business process automation.
- Automatic Purchase Order generation from PDF documents.
- Multiple interaction methods including text, voice, and document upload.
- Seamless integration with the Odoo Discuss module.
- Intelligent document processing using AI.
- Improved operational efficiency.
- Better user experience through conversational interactions.
- Reduced data entry errors.
- Quick navigation to Manufacturing Orders.
- Prevention of duplicate chatbot responses.

---

## 8. Conclusion

The **Manufacturing Chatbot Module** provides an intelligent and interactive assistant for Manufacturing operations within **Odoo 19 Community**. By combining artificial intelligence with Manufacturing workflows, the chatbot enables users to retrieve business information, automate Purchase Order creation, process PDF documents, and interact using text or voice commands.

The integration with the **Discuss** module further enhances collaboration by allowing users to communicate with the chatbot directly from their conversations. Features such as automated document processing, business query handling, duplicate request prevention, and Manufacturing Order navigation improve operational efficiency while reducing manual effort.

Overall, the Manufacturing Chatbot Module delivers a modern, AI-driven solution that simplifies Manufacturing processes, improves productivity, and provides a scalable foundation for future enhancements.
