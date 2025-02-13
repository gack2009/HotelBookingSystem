# Hotel Booking API - Clean Architecture

## 📌 Overview
This is a **Hotel Booking API** built using **ASP.NET Core** with **Entity Framework Core (EF Core)** following **Clean Architecture** principles. It allows users to:
- Find available hotels and rooms
- Book a hotel room
- Retrieve booking details
- Manage bookings

## 🏗️ Project Structure
```
/YourSolution
 ├── /YourAPIProject (Startup project, contains `Program.cs`, controllers)
 ├── /YourApplicationProject (Contains interfaces, CQRS handlers, business logic)
 ├── /YourInfrastructureProject (Contains `DbContext`, database-related logic)
 ├── /YourDomainProject (Contains entity models)
```
### 📁 **Project Breakdown**
- **API Layer (`YourAPIProject`)** → Exposes RESTful endpoints.
- **Application Layer (`YourApplicationProject`)** → Contains business logic & services.
- **Infrastructure Layer (`YourInfrastructureProject`)** → Handles database operations.
- **Domain Layer (`YourDomainProject`)** → Defines core entities (`Hotel`, `Room`, `Booking`).

---
## 🚀 Getting Started

### **1️⃣ Prerequisites**
Make sure you have:
- [.NET 7/8 SDK](https://dotnet.microsoft.com/en-us/download)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [Entity Framework Core CLI](https://learn.microsoft.com/en-us/ef/core/)

### **2️⃣ Setup Database Connection**
Modify `appsettings.json` in `YourAPIProject`:
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=HotelBookingDB;Trusted_Connection=True;TrustServerCertificate=True;"
  }
}
```

### **3️⃣ Install Dependencies**
Run the following commands:
```sh
dotnet restore
```

### **4️⃣ Run Migrations**
Run the following EF Core commands from the **solution root directory**:
```sh
dotnet ef migrations add InitialCreate --project YourInfrastructureProject --startup-project YourAPIProject
dotnet ef database update --project YourInfrastructureProject --startup-project YourAPIProject
```

### **5️⃣ Run the API**
To start the API, run:
```sh
dotnet run --project YourAPIProject
```
The API will be available at `https://localhost:5001`.

---
## 🛠️ API Endpoints

### **🏨 Hotel Endpoints**
| Method | Endpoint | Description |
|--------|---------|-------------|
| `GET` | `/api/hotels` | Get all hotels |
| `GET` | `/api/hotels/{id}` | Get hotel details by ID |

### **🛏️ Room Endpoints**
| Method | Endpoint | Description |
|--------|---------|-------------|
| `GET` | `/api/rooms/available?checkIn={date}&checkOut={date}&guests={num}` | Get available rooms |

### **📅 Booking Endpoints**
| Method | Endpoint | Description |
|--------|---------|-------------|
| `POST` | `/api/bookings` | Create a new booking |
| `GET` | `/api/bookings/{id}` | Get booking details by ID |
| `DELETE` | `/api/bookings/{id}` | Cancel a booking |

---
## ✅ Unit Testing

Unit tests are located in `YourTestsProject` and can be run using:
```sh
dotnet test
```

Mocking is done using **Moq**, and EF Core is tested using an **in-memory database**.

---
## 🛠️ Common Issues & Fixes
### **1️⃣ `dotnet ef` Command Not Found**
Run:
```sh
dotnet tool install --global dotnet-ef
```
### **2️⃣ Cannot Connect to SQL Server**
- Ensure SQL Server is **running**.
- Check that the **connection string is correct**.

### **3️⃣ Reset Migrations**
If needed, reset migrations:
```sh
dotnet ef migrations remove --project YourInfrastructureProject --startup-project YourAPIProject
dotnet ef migrations add InitialCreate --project YourInfrastructureProject --startup-project YourAPIProject
dotnet ef database update --project YourInfrastructureProject --startup-project YourAPIProject
```

---
## 📜 License
This project is licensed under the **MIT License**.

---
## 💡 Need Help?
If you have any issues, feel free to open an **issue** or reach out for support! 🚀

