# DealDekho

**Find the cheapest way to order food in India, with every offer applied.**

DealDekho is an AI agent that compares Swiggy and Zomato for the same order. You type what you want ("paneer biryani for 2 under Rs 400"), and it tells you which app, which restaurant, which coupon and which payment method gives the lowest final price.

> Demo video: [add your unlisted YouTube link here]

## Why

The menu price is never the real price. Delivery fees, platform fees, packaging, taxes, restaurant coupons and bank or UPI offers all change the final amount, and they differ between apps. Checking this by hand means opening two apps, building two carts and comparing bills. DealDekho does that in one step.

## How it works

1. **Search:** finds open restaurants near your saved address on both apps, filtered by rating, distance and budget.
2. **Build carts:** adds the matching items to a cart on each app. Nothing is ordered.
3. **Read real bills:** pulls the full bill and every available coupon and payment offer, with applicability.
4. **Compare:** works out the final payable amount for each option and respects minimum order values and discount caps.
5. **Answer:** shows the best pick, the runner-up and a table of everything checked, and leaves the winning Swiggy cart ready to pay in the app.

## Built on official APIs only

DealDekho uses the **official Swiggy MCP server** and **Zomato MCP server**, signed in with the user's own account through OAuth. It does no scraping and stores no credentials.

| App | Tools used |
|---|---|
| Swiggy | get_addresses, search_restaurants, search_menu, get_restaurant_menu, update_food_cart, get_food_cart, fetch_food_coupons, apply_food_coupon |
| Zomato | get_saved_addresses_for_user, get_restaurants_for_keyword, get_menu_items_listing, get_restaurant_menu_by_categories, create_cart |

## Safety by design

- **Never places orders or takes payments.** No checkout or payment tools are requested. The user always finishes in the official app.
- **Read-mostly:** the only writes are temporary carts used to get an accurate bill.
- **Per-user auth:** each user signs in with their own account and can disconnect at any time.
- **Low volume:** about 15 to 25 tool calls per search, only when the user asks.

## Features

- Search by dish, cuisine or restaurant, with people count, budget and veg-only filters
- Voice input
- Remembers your payment methods so bank offers are counted correctly
- History of your last 3 searches, with one-tap re-run for live prices

## Tech

- Frontend: Working Website of HTML, CSS and JavaScript (mobile-first)
- Agent: Claude (Anthropic) with tool calling over the Swiggy and Zomato MCP servers
- Current version runs inside Claude. The standalone web version (Next.js with OAuth 2.1 and PKCE) is waiting on platform access.

## Status

Working prototype, used for personal ordering. Built by Kushagra Awasthi
