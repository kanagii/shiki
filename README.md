# Shiki 四季: Japanese Omakase Restaurant Website

A sleek, dark-themed, three-page website for a fictional Edomae omakase restaurant, built with **Blazor** and **Tailwind CSS**.

## Pages

| Page | Route | Highlights |
|---|---|---|
| Home | `/` | Hero section, concept introduction, featured dishes, seasonal call-to-action |
| Menu | `/menu` | Category tabs (Omakase, Nigiri, Sashimi, Small Plates, Drinks), seasonal omakase panel |
| Reservation | `/reservation` | Validated booking form, confirmation card, location details, dining guidelines |

## Tech Stack

- **Blazor Web App** (.NET 10, Interactive Server rendering)
- **Tailwind CSS v4** (CLI build, no config file needed)
- **Google Fonts**: Cormorant Garamond (headings) and Inter (body)

## Repository Layout

The repository follows the standard .NET layout: the solution sits at the root and the actual project lives in the `AppDevMidterms/` subfolder.

```
shiki-appdev/                    ← repository root
├── AppDevMidterms/              ← the Blazor project (run all commands here)
│   ├── Components/
│   ├── Styles/
│   ├── wwwroot/
│   ├── package.json
│   └── AppDevMidterms.csproj
├── AppDevMidterms.slnx          ← Visual Studio solution
├── .gitignore
└── README.md
```

> **All `npm` and `dotnet` commands must be run inside `AppDevMidterms/`**, the folder that contains `AppDevMidterms.csproj` and `package.json`. Running them from the repository root will fail.

## Quick Start

```powershell
git clone https://github.com/kanagii/shiki-appdev.git
cd shiki-appdev\AppDevMidterms
npm install
npm run css:build
dotnet watch
```

For live styling while you edit, also run `npm run css:watch` in a second terminal. Details are in [How to Run](#how-to-run).

To open it in Visual Studio instead, double-click `AppDevMidterms.slnx` in the repository root.

## Prerequisites

Install these before running the project:

| Tool | Check with | Download |
|---|---|---|
| .NET SDK 10 | `dotnet --version` | https://dotnet.microsoft.com/download |
| Node.js (LTS) | `node --version` | https://nodejs.org |
| Git | `git --version` | https://git-scm.com |

Visual Studio 2026 is recommended, but any editor works.

## How to Run

### 1. Clone the repository

```powershell
git clone https://github.com/kanagii/shiki-appdev.git
cd shiki-appdev\AppDevMidterms
```

> `AppDevMidterms/` (inside the cloned repository) is the project folder, the one containing `AppDevMidterms.csproj` and `package.json`. Stay in it for every step below.

### 2. Install the Tailwind dependencies (first time only)

```powershell
npm install
```

### 3. Build the CSS once

```powershell
npm run css:build
```

This generates `wwwroot/tailwind.css` from `Styles/app.css`.

### 4. Start the app

Use **two terminal tabs**, both inside the project folder:

| Tab | Command | Purpose |
|---|---|---|
| 1 | `npm run css:watch` | Rebuilds Tailwind CSS whenever you save a file |
| 2 | `dotnet watch` | Runs the site with hot reload |

Then open the URL shown in the terminal (usually `http://localhost:5037`).

**In Visual Studio:** run `npm run css:watch` in the Developer PowerShell panel, then press **F5**.

## Project Structure

Contents of the `AppDevMidterms/` project folder:

```
AppDevMidterms/
├── Components/
│   ├── Layout/
│   │   └── MainLayout.razor      Navigation bar and footer
│   ├── Pages/
│   │   ├── Home.razor            /
│   │   ├── Menu.razor            /menu
│   │   └── Reservation.razor     /reservation
│   ├── Shared/
│   │   ├── SectionHeading.razor  Reusable section title
│   │   ├── DishCard.razor        Dish card with optional image
│   │   └── ImageFrame.razor      Image box that centers and crops any dimensions
│   ├── App.razor                 HTML shell and stylesheet links
│   └── Routes.razor
├── Styles/
│   └── app.css                   Tailwind entry point and theme (colors, fonts)
├── wwwroot/
│   ├── images/                   Put your photos here
│   ├── app.css                   Blazor validation and error styles
│   └── tailwind.css              Generated file, do not edit by hand
├── package.json                  Tailwind build scripts
└── Program.cs
```

## Design System

Colors are defined in `Styles/app.css` under `@theme`:

| Class suffix | Color | Use |
|---|---|---|
| `ink` | `#14110F` | Page background |
| `charcoal` | `#1F1B18` | Cards and surfaces |
| `washi` | `#F2EBDD` | Primary text |
| `mist` | `#A39B8F` | Muted text |
| `shu` | `#C8452D` | Buttons and accents |
| `gold` | `#B89B5E` | Highlights and dividers |

Example usage: `bg-ink`, `text-washi`, `border-gold`.

## Adding Images

1. Copy photos into `wwwroot/images/`.
2. Reference them with a relative path such as `images/hero.jpg`.
3. Images of any dimensions work. They are centered and cropped to fit their frame, so keep the subject near the middle of the photo.

Where to set them:

- **Home:** the `Image` value of each dish in the `dishes` list in `Home.razor`
- **Menu:** `BannerImage` and `OmakaseImage` in `Menu.razor`
- **Reservation:** `HeaderImage` in `Reservation.razor`

If no image is set, a kanji placeholder is shown instead.

## Troubleshooting

| Problem | Fix |
|---|---|
| Page looks unstyled | Make sure `npm run css:watch` is running, or run `npm run css:build` |
| `npm` or `node` not recognized | Install Node.js, then restart your terminal or Visual Studio |
| New Tailwind classes don't show | Check that `css:watch` is running, then hard refresh with Ctrl+F5 |
| `SectionHeading` or `DishCard` not found | Confirm `@using AppDevMidterms.Components.Shared` is in `Components/_Imports.razor` |
| Images don't appear | Check the file name, its case, and that it is inside `wwwroot/images/` |
| Outline box around the page title | Confirm `h1:focus { outline: none; }` is in `wwwroot/app.css` |
| `npm audit` reports vulnerabilities | Safe to ignore; they affect build tools only. Avoid `npm audit fix --force` |

## Notes

- The reservation form is **front-end only**. It validates input and shows a confirmation card, but no data is saved or emailed.
- The menu is a hard-coded list inside `Menu.razor`; no database is used.
- Restaurant name, address, phone number, and prices are placeholders.
