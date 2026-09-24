# Forkedin

A recipe-sharing social app. Browse recipes, **publish your own**, rate and comment on them, save favorites, and ask an **AI cooking assistant** questions about the recipe you're looking at.

> Four-person team project built during UNC Forge (summer 2025) with Jackson Le, Nick Nguyen and Ben ([BenjaminVC](https://github.com/BenjaminVC)). Full commit history: [Quole0812/Forkedin](https://github.com/Quole0812/Forkedin).
>
> **My part:** the recipe browse and detail experience (Edamam integration in `back/routes/RecipeDisplay.js`, plus the `RecipeDisplay` and `RecipeDetails` pages), Firebase setup on the client and server, the header and navigation, and parts of the recipe-creation endpoint.

## Features

- **Recipe feed.** Official recipes come from the [Edamam Recipe API](https://developer.edamam.com/) and are mixed with recipes that users publish.
- **Create a recipe.** A multi-ingredient form with image upload (multer → **AWS S3**), stored in Firestore.
- **Ratings & comments.** Per-recipe ratings (aggregate plus per-user) and threaded comments.
- **AI cooking assistant.** A chat for each recipe, backed by OpenAI. The recipe's name, ingredients and calories go into the system prompt, and the conversation history is saved per user per recipe in Firestore.
- **Accounts.** Firebase Auth sign-up/login, username availability check, profile page, saved recipes, "my recipes", and an admin review view.
- Protected endpoints verify Firebase ID tokens server-side.

## Architecture

```
front/forkedin   React 19 + Vite, React Router 7, MUI, Firebase Auth (client)
back/            Express 5 API on :5001
  routes/        create, RecipeDisplay (Edamam), Users, Ratings, Comments, Chat, RecipesByIds
  firebase.js    firebase-admin (Firestore + token verification)
```

## Run it locally

Backend (`back/.env`: `OPENAI_API_KEY`, `EDAMAM_APP_ID`, `EDAMAM_APP_KEY`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`; plus a Firebase service account at `back/permissions.json`):

```bash
cd back && npm install && npm start
```

Frontend (`front/forkedin/.env` with your Firebase web config):

```bash
cd front/forkedin && npm install && npm run dev   # http://localhost:5173
```

Secrets are git-ignored. You need your own keys to run it.
