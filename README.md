# 🚀 Animated Draggable Task Planner with Tailwind & Vue.js

[![Vue.js](https://img.shields.io/badge/Vue.js-2.7-green.svg)](https://vuejs.org/) [![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-3.0-blue.svg)](https://tailwindcss.com/)

## ✨ Features
- **Kanban Board**: Drag & drop tasks between dynamic columns (e.g., Backlog, In Progress).
- **Add Tasks/Tables/Dashboards**: Intuitive modals for creating tasks (with name, description, tag, quantity), columns, and dashboards.
- **Team Management**: Add members, display avatars (+16 indicator).
- **Search & Navigation**: Navbar with search, dashboard toggle.
- **Persistence**: Auto-save to localStorage.
- **Counters & Badges**: Task totals, types.
- **Reset & Remove**: Confirm dialogs for safety.
- **Responsive UI**: Tailwind CSS, sliders (VueperSlides), animations.

## 🛠 Tech Stack
- **Frontend**: Vue.js 2, vuedraggable, Bootstrap-Vue
- **Styling**: Tailwind CSS, FontAwesome icons
- **Utils**: EventBus, UUID, localStorage, modals (vue-tailwind-modal)
- **Other**: VueperSlides, confirm dialogs

## 🚀 Quick Start
1. Clone the repo:
   ```
   git clone <your-repo-url>
   cd "Task Manigar"
   ```
2. Install dependencies:
   ```
   npm install
   ```
3. Run development server (Node 17+ fix):
   ```
   npm run serve
   ```
   *Note: If Node 17+, legacy OpenSSL enabled. Update browserslist: `npx browserslist@latest --update-db`*
4. Open `http://localhost:8080` in your browser.

## 💡 Usage
1. Click `+` to add columns/tables.
2. Select table in task modal to add tasks.
3. Drag tasks between columns.
4. Use navbar for search/dashboard.
5. Reset board if needed.

## 📂 Project Structure
```
.
├── public/          # Static assets
├── src/
│   ├── components/  # Reusable UI: TaskAdder.vue, Table.vue, etc.
│   ├── App.vue      # Main board
│   └── main.js      # App entry
├── package.json     # Dependencies
└── README.md        # This file!
```

## 🤝 Contributing
1. Fork the repo.
2. Create branch: `git checkout -b feature/AmazingFeature`
3. Commit: `git commit -m 'Add AmazingFeature'`
4. Push: `git push origin feature/AmazingFeature`
5. Open PR!

## 📄 License
MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments
Built with Vue.js ecosystem. Star the repo if useful! ⭐

