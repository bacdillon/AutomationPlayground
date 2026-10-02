# Interactive Dashboard: Furniture Inventory by Room

A Power BI dashboard that tracks furniture inventory across the rooms of a home, using a floor plan style visual that lets a viewer select a specific room and instantly see exactly what furniture is in it.

## 1. Project Overview

This project is a Power BI report titled "Interactive Dashboard Furniture Inventory by Room." It presents a floor plan style layout, labeled "Interactive Areas," with each room marked out and its dimensions shown. Alongside it, a "No of furniture" summary card and a "Furniture, Sum of Quantity, Room" table give a detailed breakdown of what furniture exists in each space. The video shows the report being actively built in Power BI Desktop, with the room based filtering and calculations visible as they are put together.

## 2. Business Problem & Objectives

**The problem:** Keeping track of furniture and fittings across multiple rooms in a home or property is easy to lose track of over time. A flat spreadsheet list of furniture items does not show at a glance which room something belongs to, or make it easy to compare how furnished one room is against another. Without a visual, spatial way to view this data, reviewing or auditing furniture inventory means scrolling through rows rather than seeing the layout of the home itself.

**The objectives:**
- Represent a home's layout visually, by room, rather than as a flat list.
- Let a viewer select a specific room and see exactly which furniture items are in it.
- Summarize total furniture count, both overall and per room.
- Build the report using Power BI's data modeling and visual design tools.

## 3. Solution

The dashboard is built around three connected elements: an "Interactive Areas" visual showing the home's floor plan with each room's boundary and dimensions marked, a "No of furniture" card giving a running total, and a "Furniture, Sum of Quantity, Room" table listing each furniture item, its quantity, and the room it belongs to. Selecting a room in the floor plan filters the table and the total to reflect just that room's contents.

### What the Video Demonstrates

The report's full, unfiltered furniture list is shown first, including items such as Cabinet (Family), Light (Entrance), Plants (Bath), and multiple Rug and Table entries spread across Dining, Entrance, Kitchen, and Living rooms. The floor plan shows labeled rooms, including Family, Entrance, Bath, Dining, Kitchen, Living, and a half bath, each with its dimensions displayed (for example, "6'7 x 6'80"). Selecting the Kitchen area on the floor plan filters the table to show only that room's furniture: Rug (1), Table (1), Plants (2), and Chair (4), with a total of 8 items. The video shows this "Interactive Areas" visual being actively built and refined in Power BI Desktop, with the report's ribbon, formatting tools, and visual configuration panes visible throughout, indicating this is a development and build walkthrough rather than a finished, published end-user view.

### End-to-End Workflow, Step by Step

1. **Review the full furniture list.** The underlying table shows every furniture item, its quantity, and its assigned room.
2. **View the floor plan.** The "Interactive Areas" visual displays the home's layout, with each room labeled and dimensioned.
3. **Select a room.** Clicking or selecting a room on the floor plan filters the connected visuals to that room only.
4. **Review the filtered result.** The "Furniture, Sum of Quantity, Room" table and the "No of furniture" card update to show only the selected room's items and its total.
5. **Repeat for other rooms.** The same selection and filtering behavior applies across the home's different rooms.

## 4. Solution Architecture & Technologies

- **Microsoft Power BI Desktop**, used to build and configure the report.
- **A furniture inventory dataset**, covering furniture type, quantity, and assigned room. The specific data source was not shown in the video.
- **An "Interactive Areas" visual**, displaying the home's floor plan with labeled, dimensioned rooms, used as a spatial filter for the rest of the report.
- **A summary card visual**, showing the total furniture count.
- **A table visual**, listing furniture items by type, quantity, and room.
- **Interactive filtering**, connecting the floor plan selection to the table and summary card so they update together.

The floor plan based filtering is what distinguishes this report from a standard table or chart based dashboard. Rather than filtering through a dropdown or slicer, the viewer interacts directly with the spatial layout of the home itself, selecting a room on the plan to see what it contains. The underlying furniture data and room assignments feed both the full list and the per-room breakdown, so the same dataset powers both the overall summary and the room specific views.
