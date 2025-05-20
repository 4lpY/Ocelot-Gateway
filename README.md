
# Ocelot API Gateway

This project is a lightweight **.NET 8 API Gateway** using **Ocelot**, designed to route requests from the LLM-Communication Service to the actual **Mobile Billing API** based on intent.

---

## 🎯 Purpose

- Expose simple, friendly upstream routes like `/gateway/paybill`
- Internally forward those to the correct backend route like `/api/v1/bills/pay`
- Allow secure, modular request dispatching from AI agents

---

## 🧠 Routing Intent → API

| Intent             | Upstream Route               | Downstream API Endpoint                  |
|--------------------|------------------------------|-------------------------------------------|
| `QueryBill`        | `/gateway/querybill`         | `/api/v1/bills`                           |
| `QueryBillDetailed`| `/gateway/querybill-detailed`| `/api/v1/bills/detailed?page=1&pageSize=10` |
| `MakePayment`      | `/gateway/paybill`           | `/api/v1/bills/pay`                       |

---

## ⚙️ Configuration

All routing is defined in `ocelot.json`.

### Sample Entry

```json
{
  "DownstreamPathTemplate": "/api/v1/bills",
  "DownstreamScheme": "https",
  "DownstreamHostAndPorts": [
    {
      "Host": "alpy-mobile-billing-api.azurewebsites.net",
      "Port": 443
    }
  ],
  "UpstreamPathTemplate": "/gateway/querybill",
  "UpstreamHttpMethod": [ "POST" ]
}
```

---

## 📁 Project Structure

```
/ApiGateway
  Program.cs           → Ocelot setup
  ocelot.json          → routing rules
```

---

## 🚀 Running the Gateway

```bash
dotnet restore
dotnet run
```

Runs on: `https://localhost:5000`

> Ensure you trust the development certificate if using HTTPS locally.

---

## 🔐 Notes

- Downstream API requires valid structure and data
- You can add authentication and rate-limiting via Ocelot middleware later
- Supports chaining, request transforms, and JWT validation if needed

---

### Video Link
https://youtu.be/3O6gRAq8Scw



## 👥 Authors

Developed by **Yigit Alp YUKSEL** – SE4458 Assignment 2
