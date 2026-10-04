# Willmar AG — Event Schedule

This file controls the events shown on the Willmar AG digital events display.

You only need to edit **`events.json`** to add, remove, or update events.

The website automatically:

- Sorts events by date
- Hides events that have already ended
- Shows the next 5 events
- Handles events with multiple times
- Handles multi-day events
- Refreshes automatically every 5 minutes
- Displays times in Central Time

---

# Adding an Event

Every event goes inside the `"events"` list.

The basic format is:

```json
{
  "title": "Event Name",
  "location": "Willmar AG",
  "occurrences": [
    {
      "start": "2026-10-07T18:30:00-05:00",
      "end": "2026-10-07T20:00:00-05:00"
    }
  ]
}
```

### Example

```json
{
  "events": [
    {
      "title": "Youth Group",
      "location": "Willmar AG",
      "occurrences": [
        {
          "start": "2026-10-07T18:30:00-05:00",
          "end": "2026-10-07T20:00:00-05:00"
        }
      ]
    }
  ]
}
```

This will display approximately as:

**OCT 7**

**Youth Group**  
6:30 PM  
Willmar AG

---

# Event Fields

Each event can contain these fields:

| Field | Required? | Description |
|---|---|---|
| `title` | Yes | Name of the event |
| `location` | No | Where the event takes place |
| `description` | No | Additional information |
| `occurrences` | Yes | The date/time(s) of the event |

Example:

```json
{
  "title": "Kingdom Builders",
  "location": "Willmar AG",
  "description": "Annual Kingdom Builders offering",
  "occurrences": [
    {
      "start": "2026-11-15T10:30:00-06:00",
      "end": "2026-11-15T12:00:00-06:00"
    }
  ]
}
```

---

# Multiple Times on the Same Day

If an event happens more than once on the same day, add multiple occurrences.

For example, Sunday services:

```json
{
  "title": "Sunday Worship",
  "location": "Willmar AG",
  "occurrences": [
    {
      "start": "2026-10-04T08:30:00-05:00",
      "end": "2026-10-04T09:45:00-05:00"
    },
    {
      "start": "2026-10-04T10:30:00-05:00",
      "end": "2026-10-04T11:45:00-05:00"
    }
  ]
}
```

The display will show:

**OCT 4**

**Sunday Worship**  
8:30 AM • 10:30 AM  
Willmar AG

Both times count as **one event**.

---

# Multi-Day Events

For an event that happens across several days, add an occurrence for each day.

Example:

```json
{
  "title": "Breakaway",
  "location": "LGCC",
  "occurrences": [
    {
      "start": "2026-10-09T18:00:00-05:00",
      "end": "2026-10-09T21:00:00-05:00"
    },
    {
      "start": "2026-10-10T09:00:00-05:00",
      "end": "2026-10-10T21:00:00-05:00"
    },
    {
      "start": "2026-10-11T09:00:00-05:00",
      "end": "2026-10-11T13:00:00-05:00"
    }
  ]
}
```

The display will show:

**OCT 9–11**

**Breakaway**  
LGCC

It will **not** display every individual time because the event spans multiple days.

---

# Date and Time Format

Always use this format:

```text
YYYY-MM-DDTHH:MM:SS-05:00
```

For example:

```text
2026-10-07T18:30:00-05:00
```

This means:

**October 7, 2026 at 6:30 PM Central Time**

## Central Time

Because Willmar is in Central Time, use:

### During Daylight Saving Time

```text
-05:00
```

Example:

```text
2026-07-15T18:30:00-05:00
```

### During Standard Time

```text
-06:00
```

Example:

```text
2026-12-15T18:30:00-06:00
```

The website itself is configured for:

```text
America/Chicago
```

---

# Adding an Event Without a Specific End Time

The `end` field is optional.

If you leave it out, the website assumes the event lasts **one hour**.

For example:

```json
{
  "title": "Prayer Meeting",
  "location": "Prayer Room",
  "occurrences": [
    {
      "start": "2026-10-08T07:00:00-05:00"
    }
  ]
}
```

The website will treat this as:

**7:00–8:00 AM**

---

# Adding a Description

Descriptions are optional.

```json
{
  "title": "Summer Jam",
  "location": "Willmar AG",
  "description": "For kids entering 1st–6th grade",
  "occurrences": [
    {
      "start": "2027-06-15T18:00:00-05:00",
      "end": "2027-06-15T20:30:00-05:00"
    }
  ]
}
```

Keep descriptions short because they are displayed on a vertical TV screen.

---

# Adding Multiple Events

Put each event inside the `"events"` array, separated by commas.

Example:

```json
{
  "events": [
    {
      "title": "Sunday Worship",
      "location": "Willmar AG",
      "occurrences": [
        {
          "start": "2026-10-04T08:30:00-05:00",
          "end": "2026-10-04T09:45:00-05:00"
        },
        {
          "start": "2026-10-04T10:30:00-05:00",
          "end": "2026-10-04T11:45:00-05:00"
        }
      ]
    },

    {
      "title": "Youth Group",
      "location": "Willmar AG",
      "occurrences": [
        {
          "start": "2026-10-07T18:30:00-05:00",
          "end": "2026-10-07T20:00:00-05:00"
        }
      ]
    },

    {
      "title": "Prayer Meeting",
      "location": "Prayer Room",
      "occurrences": [
        {
          "start": "2026-10-08T07:00:00-05:00",
          "end": "2026-10-08T08:00:00-05:00"
        }
      ]
    }
  ]
}
```

---

# Important JSON Rules

JSON is picky. A single missing comma or quotation mark can prevent the events from loading.

### Use double quotation marks

Correct:

```json
"title": "Youth Group"
```

Incorrect:

```json
'title': 'Youth Group'
```

### Put commas between events

Correct:

```json
{
  "title": "Event One"
},

{
  "title": "Event Two"
}
```

There should **not** be a comma after the final event.

### Don't put a comma after the final item

Correct:

```json
"location": "Willmar AG"
```

Incorrect:

```json
"location": "Willmar AG",
```

---

# Complete Example

Here's a complete `events.json` you can use as a template:

```json
{
  "events": [
    {
      "title": "Sunday Worship",
      "location": "Willmar AG",
      "occurrences": [
        {
          "start": "2026-10-04T08:30:00-05:00",
          "end": "2026-10-04T09:45:00-05:00"
        },
        {
          "start": "2026-10-04T10:30:00-05:00",
          "end": "2026-10-04T11:45:00-05:00"
        }
      ]
    },

    {
      "title": "Youth Group",
      "location": "Willmar AG",
      "occurrences": [
        {
          "start": "2026-10-07T18:30:00-05:00",
          "end": "2026-10-07T20:00:00-05:00"
        }
      ]
    },

    {
      "title": "Breakaway",
      "location": "LGCC",
      "description": "Youth retreat",
      "occurrences": [
        {
          "start": "2026-10-09T18:00:00-05:00",
          "end": "2026-10-09T21:00:00-05:00"
        },
        {
          "start": "2026-10-10T09:00:00-05:00",
          "end": "2026-10-10T21:00:00-05:00"
        },
        {
          "start": "2026-10-11T09:00:00-05:00",
          "end": "2026-10-11T13:00:00-05:00"
        }
      ]
    },

    {
      "title": "Kingdom Builders",
      "location": "Willmar AG",
      "occurrences": [
        {
          "start": "2026-10-18T10:30:00-05:00",
          "end": "2026-10-18T12:00:00-05:00"
        }
      ]
    }
  ]
}
```

## How the Display Works

You do **not** need to manually put events in chronological order.

The website does that automatically.

You can enter:

```text
Christmas
Youth Group
Sunday Worship
Men's Breakfast
Easter
```

in any order, and the display will automatically sort them by their next upcoming date.

It will also automatically remove events after they have ended.

**You only need to maintain `events.json`.**
