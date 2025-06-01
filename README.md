# ✈️ Airport Gap API Automation with Postman

This repository demonstrates API Test Automation using [Postman](https://www.postman.com/) with real-world endpoints provided by [AirportGap](https://airportgap.com/docs). It includes automated tests for `GET`, `POST`, `PUT (PATCH)`, and `DELETE` requests, along with negative and edge test cases — executed via Postman Collection Runner.

---

## 📌 Project Overview

| Feature            | Details                                                                 |
|--------------------|-------------------------------------------------------------------------|
| 🔧 Tooling         | Postman, `pm` scripts, Postman Runner                                   |
| 📂 Test Coverage   | Authentication, Airport Info, Distance API, Favorites Management        |
| 🔁 Test Automation | Collection Runner (with Assertions, Timings, and Status validations)    |
| ❗ Negative Tests   | Extensive coverage for invalid input, missing parameters, and edge cases|
| 📄 Reports         | Collection + Runner JSON available for review                          |

---

## 🧪 Folder Structure

### 1. `Authentication`
- ✅ `POST /tokens`: Valid login
- ❌ Negative: Invalid email/password

### 2. `Airports`
- ✅ `GET /airports`: Fetch all
- ✅ `GET /airports/:id`: Fetch by airport code
- ❌ Invalid/Nonexistent airport code test

### 3. `Airports Distance`
- ✅ Valid pairs: Calculates correct distance
- ❗ Same airport codes → Distance = 0
- ❌ Invalid format or missing fields → 422 error

### 4. `Favorites`
- ✅ `POST /favorites`: Add to favorites
- ✅ `GET /favorites/:id`: Retrieve favorite
- ✅ `PATCH /favorites/:id`: Update note
- ✅ `DELETE /favorites/:id`: Delete favorite
- ❌ GET/UPDATE invalid ID → 404

---

## 🧠 Test Scripts & Highlights

### ✅ Sample `pm` Script: Validate Token
```js
pm.test("Token is a non-empty string", function () {
    const token = pm.response.json().data.token;
    pm.expect(token).to.be.a("string").and.not.empty;
});
```

### ✅ Sample Distance Calculation Check
```js
pm.test("Distance should be 0", () => {
    const distance = pm.response.json().data.attributes.kilometers;
    pm.expect(distance).to.eql(0);
});
```

---

## ⚙️ Automation with Runner

The entire suite was run using Postman Collection Runner:
- 🔄 Total Requests Run: 18
- ✅ Passed: 31 tests
- ❌ Failed: 2 (due to negative validations)
- 🕓 Avg Response Time: ~45ms

📎 Runner report exported as JSON: `Airport Gap API Automation.postman_test_run.json`

---

## 🚩 Negative & Edge Test Cases

| Test Scenario                                    | Status  | Reason |
|--------------------------------------------------|---------|--------|
| Invalid login credentials                        | ✅ Pass | Returns 401 |
| Nonexistent airport code                         | ✅ Pass | Returns 404 |
| Distance: Same `from` and `to` airport           | ✅ Pass | Returns 0 km |
| Invalid airport code format (`$$$`, `123!`)      | ✅ Pass | Returns 422 |
| GET Favorite with invalid ID                     | ✅ Pass | Returns 404 |
| PATCH Favorite with empty note                   | ✅ Handled | Returns 422 or success |

---

## 📥 How to Run

1. **Import the Collection**
   - Use `Airport Gap API Automation Collection.postman_collection.json`

2. **Set Environment**
   - Add your `Authorization` Bearer token after login

3. **Run with Collection Runner**
   - Load `Airport Gap API Automation Collection`
   - Click "Run" > Export results

4. **Review Results**
   - Check exported file: `postman_test_run.json`

---

## 📸 Screenshots


![Screenshot 2025-06-01 at 1 33 10 PM](https://github.com/user-attachments/assets/d9800bd2-48e0-45a2-a14d-ef0ebf0111b2)


> 📌 Screenshot of a successful test run with 200/201 status validations, execution timings, and custom test scripts.

---

## 🙌 Acknowledgments

- API Provider: [AirportGap](https://airportgap.com/docs)
- Testing Tool: [Postman](https://postman.com)
- Automation Inspiration: Real-world API test scenarios

---

## 📁 Files Included

| File Name                                      | Purpose                          |
|------------------------------------------------|----------------------------------|
| `Airport Gap API Automation Collection.json`   | Full Postman Collection          |
| `Airport Gap API Automation.postman_test_run.json` | Test Runner Output               |

---

## ✨ Author

**Yash Patel**   
📫 [LinkedIn](https://www.linkedin.com/in/yashpatel458)

---
