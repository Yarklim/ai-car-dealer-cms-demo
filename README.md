# AI Car Dealer CMS & Website

This project is a **fully featured, responsive car dealership website** with an integrated content management system (CMS), built on a modern technology stack. The system includes advanced search, AI-powered content automation, and a complete admin dashboard.

## 🚀 Core Technologies

* **Framework:** Next.js (App Router, Turbopack).
* **Database:** PostgreSQL with Prisma ORM.
* **Styling:** Tailwind CSS v4 and Shadcn/UI.
* **Storage:** AWS S3 for image storage.
* **Caching and Sessions:** Redis via Upstash for storing favorite listings.
* **AI Integration:** Vercel AI SDK and OpenAI for automatic vehicle data recognition from uploaded photos.

## ✨ Key Features

### For Users — Frontend

* **Advanced Filtering System:** includes cascading taxonomy filters and range-based filters such as year, price, and mileage.
* **SEO-Optimized Pagination:** configured to help search engines such as Google efficiently index individual listing pages.
* **Interactive Listings:** vehicle listing pages with an image carousel powered by Swiper API, smooth transition effects, and a fullscreen modal viewer.
* **Favorites System:** allows users to save preferred vehicles in Redis-backed sessions without requiring mandatory registration.
* **Multi-Step Reservation Flow:** a vehicle reservation form that lets users select a date, choose a time, and submit contact details.
* **Image Optimization:** uses `unlazy` and `thumbhash` to generate blurred placeholders, together with `imageix` for dynamic delivery of optimized images.

### For Administrators — CMS

* **Secure Login:** admin portal with one-time password authentication sent via email.
* **AI Listing Generator:** when photos are uploaded, the system automatically detects the vehicle make, model, year, color, and description, pre-filling most of the listing form for the administrator.
* **Analytics Dashboard:** interactive charts built with `recharts` for tracking website activity and listing views.
* **Content Management:**
  * Full CRUD operations for vehicle listings.
  * Rich Text editor powered by TinyMCE for listing descriptions.
  * Bulk image upload to S3 with drag-and-drop sorting support.
* **Customer Management:** database of subscribers and potential buyers with lifecycle tracking, including statuses such as interested, contacted, and purchased.
* **Global Logout:** allows an administrator to terminate all active sessions across all devices with a single action.