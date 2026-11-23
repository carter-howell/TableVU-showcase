# TableVU

Status: Deployed web platform | In active development

I built TableVU as a multi-restaurant online ordering platform for local businesses. Each restaurant gets its own branded website, while customers, restaurant staff, and the platform administrator work through connected ordering and management interfaces.

The goal is to make direct online ordering simple: open the menu, choose items and options, check out, and follow the order status without navigating through a traditional marketing-heavy restaurant website.

Live site: [TableVU](https://tablevu.web.app)

## Overview

TableVU combines a customer-facing menu and cart with restaurant management, a live orders dashboard, and platform administration. Restaurants share the application but have separate domains, branding, menus, access permissions, and payment connections.

The business model removes the upfront website build fee in favor of a percentage of online orders. The platform fee is configurable per restaurant. Stripe Connect handles the payment flow between the platform and the restaurant's connected account; payouts follow the account's Stripe settings rather than a manual end-of-day split.

## Customer Experience

- Compact menu rows with category navigation, food photos, prices, and restaurant-defined tags
- Sold-out states and configurable item options
- Separate cart entries for the same item with different selections
- Per-item instructions when enabled by the restaurant
- Slide-in cart with quantities, customer name, order type, and order instructions
- To Go and Dine In ordering
- Stripe-hosted checkout, with supported payment methods determined by the customer's device and payment configuration
- Saved cart and order confirmation across refreshes
- Order status updates and restaurant-controlled pickup estimates
- Mobile and desktop layouts built around the ordering flow

## Restaurant Tools

Restaurant staff sign in with Google and receive access to the restaurants assigned to their accounts.

### Menu and Settings

- Add, edit, hide, and remove menu items
- Organize categories and menu ordering
- Upload food images and update availability
- Configure prices, tags, grouped options, and optional item instruction fields
- Customize the restaurant name, logo, colors, and other branding settings
- Maintain contact details, business hours, pickup instructions, and tax rate
- Set ordering windows by day of the week
- Publish changes through the shared backend

### Orders and Payments

- Live order queue with customer details, item selections, and associated notes
- Preparing, Ready, Completed, and cancellation workflows
- Configurable pickup estimate
- Optional browser and audible order alerts while the dashboard is open, subject to browser permissions and audio restrictions
- Sales summaries, order history, and a payout ledger
- Stripe Connect onboarding, connection status, and disconnect controls
- Sandbox and live payment workflows, with payment mode selected by the platform administrator
- Refund handling connected to the order record

## Platform Administration

I built a separate administrator interface for managing the restaurants on the platform. It supports creating restaurant records, mapping domains, managing allowed owner emails, adjusting platform fees, and selecting sandbox or live payment mode.

This keeps platform-wide controls separate from the tools a restaurant uses for its own menu and orders. Restaurant owners do not need access to the platform administrator page.

## Implementation

I used Next.js, React, and TypeScript for the interface, with Firebase Authentication, Cloud Firestore, Cloud Storage, Cloud Functions, and Firebase Hosting for the backend and deployment. Stripe Connect supports restaurant onboarding and payments.

The deployed frontend uses a static Next.js export. The hostname determines which restaurant to load, and Firestore listeners deliver menu and order changes. Restaurant titles, icons, and metadata are updated for the active restaurant. This is not a fully server-rendered per-domain SEO implementation.

The payment backend creates checkout sessions, applies the restaurant's configured platform fee, and verifies Stripe webhook signatures before recording paid orders. Card entry is handled by Stripe rather than stored by TableVU. Sandbox and live payment configuration are kept separate.

Food image uploads pass through a backend workflow for validation and web optimization. Shared interface components keep the ordering experience consistent while allowing each restaurant to maintain its own identity.

## Access and Reliability

The project includes restaurant-scoped permissions, backend authorization checks, Firebase security rules, App Check enforcement on supported application endpoints, rate limiting, and audit records for sensitive operations.

These are implementation measures, not a claim that the application is immune to abuse or independently security-certified. Payment credentials, account configuration, webhook delivery, access assignments, and operating procedures still need to be maintained as part of running the service.

Order alerts depend on an open dashboard and browser behavior. They are not a closed-tab push notification service. Payment and payout availability also depend on the connected Stripe account's verification and configuration.

## What I Learned

This project gave me practice turning a restaurant website into a connected operational workflow. I worked through menu editing, cart persistence, item customizations, mobile layout constraints, live order status, and the relationship between a customer's checkout and the restaurant's order queue.

It also gave me experience with multi-tenant application design: resolving restaurant domains, isolating data, separating owner and platform permissions, and keeping branding consistent across public and staff pages.

The payment integration required thinking beyond a successful checkout screen. I worked through connected-account onboarding, configurable platform fees, sandbox versus live configuration, webhook-driven order creation, refunds, and the difference between a payment split and a bank payout.

## Ongoing Work

- Continue improving mobile usability and dashboard responsiveness
- Strengthen automated regression coverage for ordering, permissions, and payment edge cases
- Improve per-domain search metadata and server-rendered restaurant discovery
- Refine browser notification behavior and operational monitoring
- Simplify restaurant onboarding and staff training

## Repository

This is a public project showcase containing documentation only. The application source code is maintained privately.

This repository does not include application code, deployment configuration, credentials, database exports, customer orders, restaurant financial records, or private account information. It is not an installable distribution of TableVU.

## Portfolio

Live site: [TableVU](https://tablevu.web.app)

Portfolio: [Carter Howell](https://wchowellarchive.web.app)

GitHub: [carter-howell](https://github.com/carter-howell)
