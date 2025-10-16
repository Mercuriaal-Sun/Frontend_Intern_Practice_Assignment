# 🌐 Web Frontend Intern Practice Assignment: Free GenAI-Powered Dashboard

## 🚀 Objective

Build a **modern, responsive AI-powered frontend application** using **React + TailwindCSS**.  
The app should integrate with a **free or open-source GenAI API** (e.g., Hugging Face Inference API or local Ollama backend) to display AI-curated insights, summaries, or recommendations in an interactive dashboard format.

You’ll design and implement the full UI, integrate API data dynamically, and focus on performance, reusability, and visual polish.

---

## 🧠 Core Use Case

Create a **GenAI Content Dashboard** that allows users to:
1. Enter a topic or keyword.
2. Fetch AI-generated summaries, insights, or resources from a backend (or directly from a free GenAI API).
3. Display the data in a clean, card-based dashboard layout.
4. Visualize insights using simple charts or graphs.
5. Save user preferences (dark mode, layout, etc.) locally.

---

## 🧩 Recommended Tech Stack

| Component | Recommended Tools (All Free) |
|------------|-----------------------------|
| **Frontend Framework** | React 18+ |
| **Styling** | TailwindCSS |
| **Routing** | React Router DOM |
| **State Management** | Context API or Zustand |
| **Charts / Visualization** | Recharts or Chart.js |
| **API Calls** | Axios or native `fetch()` |
| **Generative AI API** | [Hugging Face Inference API (Free)](https://huggingface.co/inference-api) or [Ollama Local Model](https://ollama.ai) |
| **Optional Deployment** | [Vercel](https://vercel.com), [Netlify](https://www.netlify.com), or [Render](https://render.com) |

---

## 🪜 Step-by-Step Implementation

### **Part 1: Setup Project**

1. **Create React App (Vite recommended)**
   ```bash
   npm create vite@latest genai-dashboard --template react
   cd genai-dashboard
   npm install
   ```

2. **Install TailwindCSS**
   ```bash
   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init -p
   ```
   Update your Tailwind config:
   ```js
   content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
   theme: { extend: {} },
   plugins: [],
   ```

3. **Install Dependencies**
   ```bash
   npm install axios react-router-dom recharts
   ```

---

### **Part 2: Layout & Design**

- Create reusable components:
  - `Navbar.jsx` (with title, dark mode toggle)
  - `SearchBar.jsx` (topic input)
  - `Dashboard.jsx` (main content area)
  - `Card.jsx` (to display each AI summary)
  - `Chart.jsx` (visualization component)
  - `Footer.jsx`

Use Tailwind utility classes for responsive, clean UI:
```html
<div className="bg-gray-50 dark:bg-gray-900 min-h-screen text-gray-800 dark:text-gray-100">
```

---

### **Part 3: API Integration (Free GenAI API)**

#### Option 1: Hugging Face (Free Tier)
Use a public model like `"mistralai/Mistral-7B-Instruct-v0.2"`.

```javascript
// src/api/genai.js
import axios from "axios";

const HF_API_URL = "https://api-inference.huggingface.co/models/mistralai/Mistral-7B-Instruct-v0.2";
const HF_API_KEY = import.meta.env.VITE_HF_API_KEY;

export async function fetchAISummary(topic) {
  const headers = { Authorization: `Bearer ${HF_API_KEY}` };
  const prompt = `Summarize recent updates and insights on "${topic}" in 3 short points.`;

  const response = await axios.post(
    HF_API_URL,
    { inputs: prompt, parameters: { max_new_tokens: 200 } },
    { headers }
  );

  return response.data;
}
```

#### Option 2: Local Backend / Ollama
If interns have your backend assignment running, they can fetch from:
```javascript
await axios.post("http://localhost:8000/curate", { topic });
```

---

### **Part 4: State Management & Data Flow**

Use React Context or Zustand for state management:

```javascript
import { create } from "zustand";

export const useDashboardStore = create((set) => ({
  summaries: [],
  loading: false,
  fetchSummaries: async (topic) => {
    set({ loading: true });
    const data = await fetchAISummary(topic);
    set({ summaries: data, loading: false });
  },
}));
```

Display summaries dynamically in your `Dashboard` component:
```jsx
{summaries.map((item, index) => (
  <Card key={index} title={item.title} summary={item.summary} />
))}
```

---

### **Part 5: Visualization Component**

Use Recharts for visual insight representation:
```jsx
import { PieChart, Pie, Tooltip } from "recharts";

const Chart = ({ data }) => (
  <PieChart width={250} height={250}>
    <Pie data={data} dataKey="value" nameKey="label" fill="#3b82f6" />
    <Tooltip />
  </PieChart>
);
```

---

### **Part 6: Dark Mode & UX Enhancements**

Add dark mode toggle using Tailwind’s `dark:` utilities and React state:
```jsx
const [darkMode, setDarkMode] = useState(false);
document.documentElement.classList.toggle("dark", darkMode);
```

Other UI enhancements:
- Skeleton loading cards  
- Smooth transitions  
- Toast notifications (`react-hot-toast`)  
- Responsive grid for cards  

---

## 🧰 Folder Structure

```
src/
 ├── api/
 │   └── genai.js
 ├── components/
 │   ├── Navbar.jsx
 │   ├── SearchBar.jsx
 │   ├── Card.jsx
 │   ├── Chart.jsx
 │   └── Footer.jsx
 ├── pages/
 │   └── Dashboard.jsx
 ├── store/
 │   └── useDashboardStore.js
 ├── App.jsx
 ├── main.jsx
 └── index.css
```

---

## 🌍 Deployment (Free Options)

- **Vercel** – Fast, free React deployment  
  ```bash
  npm run build
  vercel deploy
  ```

- **Netlify** – Simple drag-and-drop or CLI deploy  
  ```bash
  netlify deploy
  ```

---

## 📦 Deliverables

1. **Public GitHub Repository** with:
   - Full React source code  
   - Clear folder structure  
   - Working API integration (backend or Hugging Face)  
   - `README.md` with setup steps and screenshots  

2. **Mandatory Requirements**
   - Responsive layout (desktop, tablet, mobile)
   - Data fetched dynamically
   - Interactive visualization
   - Clean UI (TailwindCSS)

---

## 🌟 Bonus / Stretch Goals

- **Offline Mode** using local storage cache  
- **Advanced Visualizations** using D3.js or Plotly  
- **Authentication (Free Supabase Auth)**  
- **Custom Themes** using Tailwind configuration  
- **Accessibility (a11y) Enhancements**  
- **Unit Tests** using Jest or Vitest  
- **Animated UI Transitions** with Framer Motion  

---

## 🎯 Learning Outcomes

✅ Advanced React architecture  
✅ Working with real GenAI APIs (free tier)  
✅ API data binding and state management  
✅ Dashboard design and visualization  
✅ Responsive UI with TailwindCSS  
✅ Deployment on free hosting platforms  

---

### 💡 Pro Tip

Pair this frontend with your **Backend GenAI API** project to form a complete **AI-powered full-stack app** — all built using free and open tools!

---

**End of Assignment**
