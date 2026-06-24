# Frontend - Driver Expense Calculator

React.js frontend for the driver expense calculator application.

## Setup Instructions

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Installation

1. **Install dependencies**
   ```bash
   npm install
   ```

2. **Create `.env` file**
   Copy from `.env.example` and update values:
   ```bash
   cp .env.example .env
   ```

3. **Configure environment variables**
   ```
   REACT_APP_API_URL=http://localhost:5000
   ```

4. **Start development server**
   ```bash
   npm start
   ```
   Application will open on `http://localhost:3000`

## Features

### Authentication
- **Register** - Create new account with personal and vehicle information
- **Login** - Secure login with JWT tokens
- **Profile** - View and update personal information

### Expense Management
- **Add Expense** - Record new expenses with category, date, amount, and notes
- **View Expenses** - List all expenses with filtering and search
- **Delete Expense** - Remove expenses from record
- **Categories** - Fuel, Maintenance, Tolls, Parking, Insurance, Other

### Dashboard
- **Summary Cards** - Total expenses and number of entries
- **Category Breakdown** - See expenses by category
- **Recent Expenses** - View latest 5 expense entries

### Summary & Analytics
- **Date Range Filter** - Filter expenses by date
- **Category Analytics** - Breakdown of expenses by category
- **Visual Progress Bars** - Percentage distribution of expenses
- **Expense Statistics** - Total amount and count metrics

## Pages

1. **Login** (`/login`) - User authentication
2. **Register** (`/register`) - New user registration
3. **Dashboard** (`/dashboard`) - Home page with overview
4. **Add Expense** (`/add-expense`) - Form to add new expense
5. **Expenses** (`/expenses`) - List of all expenses with filters
6. **Summary** (`/summary`) - Analytics and breakdown
7. **Profile** (`/profile`) - User profile management

## Project Structure

```
frontend/
├── public/
│   └── index.html
├── src/
│   ├── pages/
│   │   ├── LoginPage.js
│   │   ├── RegisterPage.js
│   │   ├── Dashboard.js
│   │   ├── AddExpense.js
│   │   ├── ExpenseList.js
│   │   ├── Summary.js
│   │   └── Profile.js
│   ├── components/
│   │   └── Navbar.js
│   ├── utils/
│   │   └── api.js
│   ├── App.js
│   ├── index.js
│   └── index.css
├── package.json
├── .env.example
└── README.md
```

## Build for Production

```bash
npm run build
```

This creates an optimized production build in the `build/` folder.

## Deployment

### Using Vercel
1. Install Vercel CLI: `npm install -g vercel`
2. Deploy: `vercel`
3. Follow the prompts

### Using Netlify
1. Build the project: `npm run build`
2. Deploy the `build/` folder to Netlify

## Environment Variables

- `REACT_APP_API_URL` - Backend API base URL (default: http://localhost:5000)

## Technologies Used

- **React.js** - UI framework
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **Tailwind CSS** - Styling
- **Chart.js** - Data visualization (ready to use)
- **date-fns** - Date manipulation
- **Lucide React** - Icons (optional)

## Available Scripts

- `npm start` - Run development server
- `npm run build` - Create production build
- `npm test` - Run tests
- `npm run eject` - Eject from Create React App (irreversible)

## API Integration

The app communicates with the backend API using the `api.js` utility. All requests automatically include the JWT token from localStorage.

### Authentication Endpoints
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/profile` - Get current user
- `PUT /api/auth/profile` - Update profile

### Expense Endpoints
- `POST /api/expenses` - Create expense
- `GET /api/expenses` - Get all expenses
- `DELETE /api/expenses/:id` - Delete expense
- `GET /api/expenses/summary/stats` - Get summary

## Troubleshooting

- **API connection errors**: Ensure backend is running on the correct port
- **CORS errors**: Check backend CORS configuration
- **Auth errors**: Clear localStorage and login again
- **Blank page**: Check browser console for errors
