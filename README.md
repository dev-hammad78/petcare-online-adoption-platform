# PetCare - Online Pet Adoption Platform (Frontend Prototype)

> **Find your forever friend.**

PetCare is a college project: a frontend-only website where people can browse adoptable pets, and (in later stages) where shelters and an admin manage listings. It is built with plain **HTML5, CSS3 and vanilla JavaScript**. There is **no backend, no database and no real authentication** yet.

## Project status

This README describes what exists **right now**. The project is being built in stages.

| Stage | Content | Status |
|-------|---------|--------|
| 1 | Shared CSS/JS, mock data, Home, Find Pets, Pet Details, How It Works, About | Built |
| 2 | Login and Register pages with a demo role selector | Built |
| 3 | Admin dashboard (5 pages) | **Not built yet** |
| 4 | Shelter dashboard (5 pages) | **Not built yet** |
| 5 | Adopter dashboard (5 pages) | **Not built yet** |

Because the dashboards do not exist yet, logging in successfully redirects to a dashboard page that is missing (you will see a "file not found" error). See [Limitations](#limitations).

## Objectives

- Practise HTML, CSS and JavaScript on a realistic multi-page project.
- Keep the code simple enough to read, explain and modify.
- Organise the frontend so it can later connect to a Java Spring Boot backend and a MySQL database.

## Features implemented so far

### Public website
- **Home** (`index.html`): hero section, pet search bar (animal type, breed, location), six featured pets, three-step adoption process, benefits, sample testimonials, sample statistics, call to action and footer.
- **Find a Pet** (`find-pets.html`): pet cards with search by name or breed; filters for species, age group, gender and location; sorting by name or age; a clear-filters button; an empty state; a favourite (heart) button on every card; a link to each pet's details.
- **Pet Details** (`pet-details.html`): loads the chosen pet from the sample data using the address (`?id=3`). Shows photo, facts, description, temperament, sample health information, shelter details, adoption information, similar pets, a favourite button and an **Apply to Adopt** form.
- **How It Works** (`how-it-works.html`) and **About** (`about.html`): static information pages.

### Login and Register (demo)
- **Register** (`register.html`): full name, email, password, confirm password and role (Adopter or Shelter), with validation and error messages.
- **Login** (`login.html`): email and password with validation, plus "Continue as Admin / Shelter / Adopter" demo buttons.

### Shared behaviour (all pages)
- Responsive layout (desktop, tablet, mobile) with a collapsible mobile menu.
- Success and error toast messages.
- Confirmation dialog helper (`confirmAction`) built on the browser's `<dialog>` element. It is ready for the dashboards but not used by any current page.
- A paw placeholder is shown when a pet photo file is missing.

## User roles

| Role | Planned purpose | Current state |
|------|-----------------|---------------|
| **Visitor** (not logged in) | Browse pets, view details, favourite pets, send a demo application | Works |
| **Adopter** | Track applications, manage profile and favourites | Can register and log in; **dashboard not built** |
| **Shelter** | Manage pets, review applications, send messages | Can register and log in; **dashboard not built** |
| **Admin** | Manage users, approve listings, settings, analytics | Demo login only; **dashboard not built** |

## Prerequisites

- A modern web browser (Chrome, Edge, Firefox or Safari).
- Optional: [Visual Studio Code](https://code.visualstudio.com/) with the **Live Server** extension.
- An internet connection is recommended so Google Fonts can load. Without it the site uses fallback fonts.

You do **not** need Node.js, npm or any build step.

## How to run the frontend locally

**Option A: open the file directly**
1. Unzip the project so you have a `PetCare` folder.
2. Double-click `index.html`.

**Option B: VS Code Live Server (recommended)**
1. Open VS Code, choose File, then Open Folder, and select `PetCare`.
2. Install the **Live Server** extension if you have not already.
3. Right-click `index.html` and choose **Open with Live Server**.

The code does not use ES modules, so it works with both options.

## Adding pet photos

No photographs are included. Put your own images in `assets/images/` using exactly these names:

`hero.jpg`, `bruno.jpg`, `luna.jpg`, `max.jpg`, `milo.jpg`, `daisy.jpg`, `coco.jpg`, `rocky.jpg`, `bella.jpg`, `charlie.jpg`, `pepper.jpg`, `oliver.jpg`, `sunny.jpg`

- Pet photos that are missing show a paw placeholder.
- `hero.jpg` (home page) has **no fallback**, so a missing file shows a broken image.
- Check the licence of any photo you download and credit the source if required.

## Using the demo login

Login is a demonstration only.

- On `login.html`, click **Continue as Admin / Shelter / Adopter** to sign in as a sample user, or type one of these emails with the password `demo1234`:
  - `admin@petcare.demo`
  - `shelter@petcare.demo`
  - `adopter@petcare.demo`
- Accounts created on the Register page are saved in the browser's localStorage. The password is **not** stored, and a registered account is recognised by email only.
- The "logged in" user is kept in `sessionStorage` and is cleared when the tab closes.

## Folder structure

```
PetCare/
├── index.html
├── find-pets.html
├── pet-details.html
├── how-it-works.html
├── about.html
├── login.html
├── register.html
├── css/
│   ├── style.css          shared styles and colour variables
│   └── responsive.css     tablet and mobile rules
├── js/
│   ├── mock-data.js       sample pets, shelters and demo users
│   ├── main.js            shared helpers used by every page
│   ├── pets.js            pet cards, search, filters, details, apply form
│   └── auth-demo.js       demo login and register
├── assets/
│   └── images/            put your photos here (not included)
├── README.md
└── .gitignore
```

Files for the Admin, Shelter and Adopter dashboards (`admin-*.html`, `shelter-*.html`, `adopter-*.html`, `dashboard.css`, `admin.js`, `shelter.js`, `adopter.js`) have **not been created yet**.

## Key files explained

- **`css/style.css`**: the colour palette and other design values are variables at the top (`:root`). Change a variable and it updates everywhere.
- **`js/mock-data.js`**: one object, `PetCareData`, holding the sample data. It is a normal script, so it works from `file://`. Pages read it directly.
- **`js/main.js`**: mobile menu, `showToast()`, `confirmAction()`, favourites functions and the missing-image fallback.
- **`js/pets.js`**: builds pet cards, filters and sorts the list, loads pet details and saves demo applications. Each page only runs the part it needs.
- **`js/auth-demo.js`**: validation and the demo session for the login and register pages.

Script order matters: `mock-data.js`, then `main.js`, then the page-specific file.

## How mock data and localStorage work

- **Pets, shelters and demo users** come from `mock-data.js` and reset to the same sample list every time the page loads. Nothing you do changes this file.
- **Favourites** are saved in `localStorage` under `petcare_favourites` as a list of pet IDs.
- **Applications** sent from the Pet Details page are saved in `localStorage` under `petcare_applications`. No page displays them yet (the adopter and shelter pages that would show them are not built).
- **Registered accounts** are saved under `petcare_users`.
- **Login session** is saved in `sessionStorage` under `petcare_session`.

localStorage lives in one browser on one computer. Clearing browser data removes it, and it is not shared between devices. To reset the demo, clear the site data in your browser's developer tools.

## Implemented functionality summary

- Search, five filters, sorting and clear filters on the pet list
- Favourite and unfavourite pets (saved in localStorage)
- Pet details loaded by ID, with similar pets
- Demo adoption application with validation
- Registration and login forms with validation
- Responsive navigation and layouts
- Toast notifications

## Limitations

- **Dashboards are not built.** Logging in redirects to `admin-dashboard.html`, `shelter-dashboard.html` or `adopter-dashboard.html`, which do not exist yet.
- **No real security.** Frontend login cannot protect anything. Anyone can edit browser storage or open any page directly. Dashboard pages are not protected.
- **No backend or database.** Data is sample data plus browser storage.
- **Applications and favourites are not shown anywhere except the card hearts.** Saved applications cannot be viewed yet.
- **No photographs included.** You must add them.
- **Not fully tested.** The home page has been opened in a browser and renders. The JavaScript files pass a syntax check, and links were checked by script. A full manual test of every filter, form and screen size has **not** been done.
- Fonts need an internet connection; otherwise fallback fonts are used.

## Future: Java Spring Boot and MySQL

The frontend is organised so it can be connected later. This is a plan, not something that exists.

**Backend (planned)**
- Spring Boot with Spring Web, Spring Data JPA, MySQL Driver, Validation and Spring Security.
- Layers: Entity, Repository, Service, Controller.
- MySQL tables such as `users`, `shelters`, `pets`, `applications`, `messages` and `favourites`, based on the shape of `mock-data.js`.

**Real authentication**
- Hash passwords with BCrypt, use JWT or sessions, and check roles on the server.

**Connecting the frontend**
- Replace reads from `PetCareData` with `fetch()` calls such as `fetch("http://localhost:8080/api/pets")`.
- Replace localStorage favourites and applications with API calls.
- Enable CORS in Spring Boot for the frontend's address.
- Add an image upload endpoint and store photo paths in MySQL.

**Suggested order:** pets (list, details, add), users and login, applications, favourites and messages, then admin features.

## Troubleshooting

- **Pet cards show a paw instead of a photo:** the image file is missing or misnamed. Check the name and that it is in `assets/images/`.
- **Home page shows a broken image:** add `assets/images/hero.jpg`.
- **Page looks unstyled or buttons do nothing:** check the `css/` and `js/` folders are directly inside `PetCare` and not nested in another `PetCare` folder.
- **After login you see "file not found":** expected until the dashboards are built.
- **Favourites or demo data seem stuck:** clear the site's localStorage in your browser's developer tools (Application tab).
- **Fonts look different:** you may be offline.
