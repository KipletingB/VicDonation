# VicFood Rescue — Two Interlinked Websites

This solution contains **two separate ASP.NET Core Razor Pages websites** and one shared data project.

## 1. VicFoodRescue.AidPortal
Runs at: `http://localhost:5101`

For people seeking food aid:
- Register with contact details, suburb, household size and Victorian region.
- Browse currently available food.
- Listings from the recipient's own region are prioritised as **Nearby**.
- View supermarket/restaurant address and public phone number.
- Open the pickup location in Google Maps.
- Reserve a pickup.
- View and cancel current reservations.

## 2. VicFoodRescue.PartnerPortal
Runs at: `http://localhost:5102`

For supermarkets and restaurants:
- Register a new business.
- Select one of the 46 preloaded Victorian businesses.
- Post available food.
- Edit listings while still available.
- See the recipient who reserved an item.
- Mark pickup as collected.
- Complete the reservation.

## 3. VicFoodRescue.Shared
Contains:
- Entity Framework Core models.
- Shared `AppDbContext`.
- Victorian regions.
- Database seeding.

## How the two websites are interlinked

Both websites connect to the exact same SQLite file in the solution folder:

`vicfoodrescue_linked.db`

Flow:

Partner Portal -> posts food -> shared SQLite database -> Aid Portal shows food

Aid Portal -> recipient reserves food -> shared SQLite database -> Partner Portal sees recipient/pickup

## Visual Studio setup

1. Extract the ZIP.
2. Open `VicFoodRescue.sln`.
3. Allow NuGet packages to restore.
4. Right-click the solution -> **Configure Startup Projects**.
5. Select **Multiple startup projects**.
6. Set both:
   - `VicFoodRescue.AidPortal` = Start
   - `VicFoodRescue.PartnerPortal` = Start
7. Run.

The browser should open:
- Aid site: `http://localhost:5101`
- Partner site: `http://localhost:5102`

## Database

A new database file is created automatically. No SQL Server or LocalDB is required.

If you have been testing older versions, this solution deliberately uses the new file name `vicfoodrescue_linked.db` to avoid schema conflicts.

## Academic prototype note

The websites use session-based selection/registration for simplicity. A production deployment should add ASP.NET Core Identity, password authentication, identity verification, authorisation roles, privacy controls, food-safety validation, rate limiting, audit logs and abuse-prevention controls.
