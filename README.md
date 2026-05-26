# CustomCalendar
A lightweight, high-performance .NET 10 backend API for calendar scheduling, recurrence expansion, resource (column) calendars, and standard iCalendar (.ics) feeds. Designed to serve JavaScript calendar widgets (FullCalendar, DayPilot) and automated consumers.

Key features

- REST API endpoints for reading, creating, moving, resizing and exporting events
- Recurrence expansion engine that evaluates recurring events and exceptions
- Resource (column) calendars and a resource tree for room/asset booking
- FullCalendar and DayPilot friendly DTOs and endpoints
- iCalendar (.ics) feed export with optional secure token access
- Time zone aware normalization and all-day event handling (uses TimeZoneConverter)
- Background purge/cleanup worker for stale data
- DB-backed persistence via CalendarDbContext (EF Core)
- Request rate limiting, CORS policy for client apps, and validation using FluentValidation
- Audit and soft-delete interceptors for consistent modification/audit tracking

Types of calendars supported

- Personal calendars (single-user events)
- Shared calendars (team calendars with resource columns)
- Resource/room calendars (huddle rooms, conference rooms, equipment)
- All-day and time-specific events
- Recurring events with exceptions (instances can be overridden or deleted)
- Read-only calendar feeds (.ics) for subscription and sync

Services and components

- AdvancedCalendarService: recurrence expansion and calendar view generation
- CalendarDbContext: EF Core database context and persistence
- CalendarPurgeBackgroundService: hosted service to purge or archive old items
- FullCalendarResourceTreeBuilder: builds hierarchical resource trees for clients
- ICalendarAuthService: token-based feed authentication for exported .ics feeds
- SoftDeleteInterceptor / UpdateAuditFieldsInterceptor: data lifecycle and audit hooks
- Validators: request/DTO validators (FluentValidation)

Integration & automation potential

- Easily consumed by FullCalendar and DayPilot frontends for interactive UIs
- .ics feed endpoint can be polled or subscribed to by external systems for synchronization
- HTTP API enables automation: create/update/move events from scripts, CI jobs, or other services
- Token-protected feed makes it suitable for automated distribution to calendar aggregators
- Can be integrated into scheduled workflows (e.g., provisioning, reporting, notifications)

Quick start

1. Configure appsettings.json / connection string for your SQL Server (or other supported provider).
2. Set CalendarCleanupSettings in configuration when using the background purge service.
3. Build and run with .NET 10 SDK: dotnet build && dotnet run
4. Point your FullCalendar or DayPilot client to the provided API endpoints and CORS origin.

Notes

- The backend uses standard libraries (EF Core, Ical.Net, TimeZoneConverter) and is prepared for production features like rate limiting and background workers, but you should secure authentication and adjust CORS and rate-limit policies for your environment.

License

- Add license information for your project repository as appropriate.
