# Exercise 3.6 - Optimized Project Images

Return to the frontend and backend Dockerfiles from exercises 1.12 and 1.13.

Keep the base images as they were: **ubuntu** for the frontend, **ubuntu or golang** for the backend.

Optimize by:
- Joining RUN commands
- Removing useless parts after build

Hints:
- Frontend: `src/` folder is not needed after `npm run build` (static files go to `build/`)
- Backend: cache is not needed

Submit:
1. Image sizes **before** and **after** the optimization
2. Your optimized Dockerfiles
