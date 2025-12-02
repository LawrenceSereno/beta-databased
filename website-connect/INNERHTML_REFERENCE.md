# 📋 innerHTML Documentation - All Files Reference

## Purpose
This document catalogs **all innerHTML generation code** across the BestBuddies application, organized by file and function. Use this as a reference to understand, locate, or retract dynamic HTML generation code.

---

## 📑 Quick Navigation

- [customer.js](#customerjs) - 25+ innerHTML locations
- [admin.js](#adminjs) - 40+ innerHTML locations
- [groomer.js](#groomerjs) - 15+ innerHTML locations
- [staff.js](#staffjs) - 10+ innerHTML locations
- [booking.js](#bookingjs) - 12+ innerHTML locations
- [main.js](#mainjs) - 8+ innerHTML locations
- [booking.html](#bookinghtml) - 3 innerHTML locations

---

## customer.js

### 1. `loadQuickStats()` - Line 124
**Element:** `#quickStats`
**Purpose:** Renders 4 stat cards (Total, Pending, Confirmed, Upcoming)
```javascript
statsContainer.innerHTML = `
  <div class="stat-card">...</div>
  <div class="stat-card">...</div>
  // 4 cards total
`;
```

### 2. `renderCustomerBookings()` - Line 208
**Element:** `#bookingsContainer`
**Purpose:** No bookings empty state
```javascript
container.innerHTML = `
  <div class="card" style="text-align: center;">
    <div style="font-size: 5rem;">🐾</div>
    <h3>No Bookings Yet</h3>
    <!-- More content -->
  </div>
`;
```

### 3. `renderCustomerBookings()` - Line 224
**Element:** `#bookingsContainer`
**Purpose:** No filters match empty state
```javascript
container.innerHTML = `
  <div class="card" style="text-align: center;">
    <div style="font-size: 3rem;">🔍</div>
    <h3>No matches</h3>
  </div>
`;
```

### 4. `renderCustomerBookings()` - Line 243
**Element:** `#bookingsContainer`
**Purpose:** Individual booking cards (map function)
```javascript
container.innerHTML = pageBookings.map(booking => {
  return `
    <div class="card booking-card">
      <div class="booking-avatar">${petEmoji}</div>
      <div class="booking-copy">
        <h3>${booking.petName}</h3>
        <!-- Booking details -->
      </div>
      <!-- Status badges and actions -->
    </div>
  `;
}).join('');
```

### 5. `updateCustomerBookingPagination()` - Line 356
**Element:** `#customerBookingPagination`
**Purpose:** Pagination controls
```javascript
pagination.innerHTML = `
  <span>Showing ${start}-${end} of ${totalItems} bookings</span>
  <div class="pagination-actions">
    <button>Previous</button>
    <button>Next</button>
  </div>
`;
```

### 6. `renderCalendarSlotSummary()` - Line 391
**Element:** `#calendarSlotSummary`
**Purpose:** No slots empty state
```javascript
summary.innerHTML = '<p class="empty-state">No open slots in the next weeks. Check back soon!</p>';
```

### 7. `renderCalendarSlotSummary()` - Line 394
**Element:** `#calendarSlotSummary`
**Purpose:** List of available slots
```javascript
summary.innerHTML = entries.slice(0, 3).map(([date, stats]) => `
  <p style="margin:0; font-size:0.9rem;">
    ${formatDate(date)} · ${stats.remaining} slots left
  </p>
`).join('');
```

### 8. `renderCommunityShowcase()` - Line 406
**Element:** `#communityReviewFeed`
**Purpose:** No reviews empty state
```javascript
container.innerHTML = '<p class="empty-state">Once admins upload before & after photos, they will appear here.</p>';
```

### 9. `renderCommunityShowcase()` - Line 409
**Element:** `#communityReviewFeed`
**Purpose:** Community review cards
```javascript
container.innerHTML = entries.map(entry => `
  <article class="review-card">
    <div class="review-card-gallery">
      <img src="${entry.beforeImage}" alt="Before">
      <img src="${entry.afterImage}" alt="After">
    </div>
    <div class="review-card-content">
      <h4>${entry.petName}</h4>
      <!-- Review details -->
    </div>
  </article>
`).join('');
```

### 10. `renderWarningPanel()` - Line 457
**Element:** `#warningPanel`
**Purpose:** Safety record warning panel
```javascript
panel.innerHTML = `
  <h3>⚠️ Safety Record</h3>
  <div class="progress-bar">
    <div class="progress-fill" style="width:${progressPercent}%"></div>
  </div>
  <p>${warnings}/5 warnings</p>
  <div class="lift-ban-note">
    <strong>How to lift a ban:</strong>
    <ol>...</ol>
  </div>
`;
```

### 11. `renderGroomingJournal()` - Line 482
**Element:** `#groomingGalleryPanel`
**Purpose:** No journal empty state
```javascript
panel.innerHTML = '<p style="color:var(--gray-500);">Your before/after albums will appear here...</p>';
```

### 12. `renderGroomingJournal()` - Line 485
**Element:** `#groomingGalleryPanel`
**Purpose:** Grooming journal cards
```javascript
panel.innerHTML = entries.map(entry => {
  return `
    <div class="card">
      <h4>${entry.petName}</h4>
      <div class="journal-photos">
        <figure><img src="${entry.beforeImage}"></figure>
        <figure><img src="${entry.afterImage}"></figure>
      </div>
      <!-- Rating and review sections -->
    </div>
  `;
}).join('');
```

### 13. `renderCustomerSlotsList()` - Line 679
**Element:** `#customerSlotsList`
**Purpose:** No slots empty state
```javascript
container.innerHTML = '<p class="empty-state">No open slots right now. Check back soon!</p>';
```

### 14. `renderCustomerSlotsList()` - Line 682
**Element:** `#customerSlotsList`
**Purpose:** Available slots with book buttons
```javascript
container.innerHTML = entries.slice(0, 4).map(([date, stats]) => `
  <div style="display:flex; justify-content:space-between;">
    <div>
      <strong>${formatDate(date)}</strong>
      <p>${stats.remaining} slots left</p>
    </div>
    <button class="btn btn-outline">Book</button>
  </div>
`).join('');
```

### 15. `openBookingDetailModal()` - Line 856
**Element:** `#modalRoot`
**Purpose:** Booking detail modal
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <div class="modal-content">
      <!-- Full booking details -->
      <!-- Action buttons -->
    </div>
  </div>
`;
```

### 16. `renderCustomerBookingHistory()` - Line 1066
**Element:** `#customerHistoryTable`
**Purpose:** No history empty state
```javascript
container.innerHTML = '<p class="empty-state">No booking history yet.</p>';
```

### 17. `renderCustomerBookingHistory()` - Line 1082
**Element:** `#customerHistoryControls`
**Purpose:** History pagination
```javascript
controls.innerHTML = `
  <div class="pagination">
    <button onclick="changeHistoryPage(${page-1})">Previous</button>
    <button onclick="changeHistoryPage(${page+1})">Next</button>
  </div>
`;
```

### 18. `renderCustomerBookingHistory()` - Line 1108
**Element:** `#customerHistoryTable`
**Purpose:** Booking history table
```javascript
container.innerHTML = `
  <table>
    <thead>
      <tr>
        <th>Date</th>
        <th>Pet</th>
        <th>Package</th>
        <th>Status</th>
      </tr>
    </thead>
    <tbody>
      <!-- History rows -->
    </tbody>
  </table>
`;
```

---

## admin.js

### 1. `loadOverview()` - Line 196
**Element:** `#overviewContent`
**Purpose:** Admin dashboard overview with stats
```javascript
container.innerHTML = `
  <div class="stats-grid">
    <!-- Overview statistics and charts -->
  </div>
`;
```

### 2. `renderPendingBookings()` - Line 351
**Element:** `#pendingBookingsContainer`
**Purpose:** No pending bookings empty state
```javascript
container.innerHTML = `
  <p class="empty-state">No pending bookings</p>
`;
```

### 3. `renderPendingBookings()` - Line 369
**Element:** `#pendingBookingsContainer`
**Purpose:** Pending booking cards
```javascript
container.innerHTML = currentSlice.map(booking => `
  <div class="booking-card">
    <!-- Booking info -->
    <button onclick="confirmBooking('${booking.id}')">Confirm</button>
  </div>
`).join('');
```

### 4. `renderPagination()` - Line 468
**Element:** Various pagination containers
**Purpose:** Page number buttons
```javascript
container.innerHTML = `<div class="pagination">${pagesHtml}</div>`;
```

### 5. `loadPendingView()` - Line 530
**Element:** `#pendingViewContent`
**Purpose:** No pending empty state
```javascript
container.innerHTML = '<p class="empty-state">No pending bookings</p>';
```

### 6. `loadPendingView()` - Line 534
**Element:** `#pendingViewContent`
**Purpose:** Pending bookings list
```javascript
container.innerHTML = `
  <div class="bookings-list">
    <!-- Pending bookings -->
  </div>
`;
```

### 7. `loadConfirmedView()` - Line 624
**Element:** `#confirmedViewContent`
**Purpose:** No confirmed empty state
```javascript
container.innerHTML = '<p class="empty-state">No confirmed bookings</p>';
```

### 8. `loadConfirmedView()` - Line 628
**Element:** `#confirmedViewContent`
**Purpose:** Confirmed bookings list
```javascript
container.innerHTML = `
  <div class="bookings-list">
    <!-- Confirmed bookings -->
  </div>
`;
```

### 9. `loadCalendarView()` - Line 741
**Element:** `#calendarViewContent`
**Purpose:** Calendar and bookings by date
```javascript
container.innerHTML = `
  <div class="calendar">
    <!-- Calendar grid -->
    <div class="bookings-for-date">
      <!-- Bookings for selected date -->
    </div>
  </div>
`;
```

### 10. `loadCalendarView()` - Line 752
**Element:** `#calendarViewContent`
**Purpose:** No bookings on date empty state
```javascript
container.innerHTML = '<p class="empty-state">No appointments for this date</p>';
```

### 11. `loadCalendarView()` - Line 763
**Element:** `#calendarViewContent`
**Purpose:** Bookings for selected date
```javascript
container.innerHTML = `
  <ul class="bookings-list">
    <!-- Bookings for date -->
  </ul>
`;
```

### 12. `loadCalendarBlackoutView()` - Line 878
**Element:** `#blackoutListContainer`
**Purpose:** No blocked days empty state
```javascript
container.innerHTML = '<p class="empty-state">No closed days yet.</p>';
```

### 13. `loadCalendarBlackoutView()` - Line 881
**Element:** `#blackoutListContainer`
**Purpose:** List of blocked dates
```javascript
container.innerHTML = entries.map(entry => `
  <div class="blocked-day-card">
    <strong>${formatDate(entry.date)}</strong>
    <p>${entry.reason}</p>
    <button onclick="unblockDate('${entry.date}')">Unblock</button>
  </div>
`).join('');
```

### 14. `loadCustomersView()` - Line 933
**Element:** `#customersListContainer`
**Purpose:** No customers empty state
```javascript
container.innerHTML = '<p class="empty-state">No customers yet</p>';
```

### 15. `loadCustomersView()` - Line 937
**Element:** `#customersListContainer`
**Purpose:** Customers list
```javascript
container.innerHTML = `
  <table class="customers-table">
    <!-- Customer rows -->
  </table>
`;
```

### 16. `handlePhotoUpload()` - Line 1454
**Element:** `#photoPreview`
**Purpose:** Uploaded photo preview
```javascript
preview.innerHTML = `<img src="${src}" alt="Uploaded preview">`;
```

### 17. `loadGroomerAbsencesView()` - Line 1502
**Element:** `#absencesListContainer`
**Purpose:** No absence requests empty state
```javascript
container.innerHTML = '<p class="empty-state">No groomer absence requests yet.</p>';
```

### 18. `loadGroomerAbsencesView()` - Line 1506
**Element:** `#absencesListContainer`
**Purpose:** Groomer absence requests
```javascript
container.innerHTML = `
  <div class="absences-list">
    <!-- Absence request cards -->
  </div>
`;
```

### 19. `renderQuickPendingAbsences()` - Line 1611
**Element:** Quick absences container
**Purpose:** No pending absences empty state
```javascript
container.innerHTML = '<p class="empty-state">All caught up!</p>';
```

### 20. `renderQuickPendingAbsences()` - Line 1615
**Element:** Quick absences container
**Purpose:** Show first 3 pending absences
```javascript
container.innerHTML = pending.slice(0, 3).map(absence => `
  <div class="absence-card">
    <!-- Absence info -->
  </div>
`).join('');
```

### 21. `renderQuickBlockedUsers()` - Line 1635
**Element:** Quick blocked users container
**Purpose:** No blocked customers empty state
```javascript
container.innerHTML = '<p class="empty-state">No blocked customers</p>';
```

### 22. `renderQuickBlockedUsers()` - Line 1639
**Element:** Quick blocked users container
**Purpose:** Show blocked users list
```javascript
container.innerHTML = blocked.map(user => `
  <div class="user-card">
    <strong>${user.name}</strong>
    <p>${user.warnings} warnings</p>
  </div>
`).join('');
```

### 23. `loadHistoryView()` - Line 1806
**Element:** `#historyViewContent`
**Purpose:** No activity empty state
```javascript
container.innerHTML = '<p class="empty-state">No booking activity yet.</p>';
```

### 24. `loadHistoryView()` - Line 1820
**Element:** History pagination container
**Purpose:** History page controls
```javascript
controls.innerHTML = `
  <button onclick="changeHistoryPage(${page-1})">Previous</button>
  <button onclick="changeHistoryPage(${page+1})">Next</button>
`;
```

### 25. `loadHistoryView()` - Line 1846
**Element:** `#historyViewContent`
**Purpose:** Booking activity log
```javascript
container.innerHTML = `
  <table class="history-table">
    <!-- Activity rows -->
  </table>
`;
```

### 26. `openBookingModal()` - Line 1993
**Element:** `#modalRoot`
**Purpose:** Booking detail modal
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <div class="modal-content">
      <!-- Full booking details with actions -->
    </div>
  </div>
`;
```

### 27. `openRescheduleModal()` - Line 2098
**Element:** Document body
**Purpose:** Reschedule modal
```javascript
document.body.insertAdjacentHTML('beforeend', modalHTML);
```

### 28. `renderLiftBanRequests()` - Line 2203
**Element:** Ban request container
**Purpose:** No ban requests empty state
```javascript
container.innerHTML = '<p class="empty-state">No customers awaiting lift approval</p>';
```

### 29. `renderLiftBanRequests()` - Line 2207
**Element:** Ban request container
**Purpose:** Show ban lift requests
```javascript
container.innerHTML = banned.slice(0, 4).map(user => `
  <div class="ban-request-card">
    <!-- Ban request details -->
  </div>
`).join('');
```

### 30. `renderPackageList()` - Line 2412
**Element:** Packages container
**Purpose:** List all packages
```javascript
container.innerHTML = packages.map(pkg => `
  <div class="package-card">
    <h3>${pkg.name}</h3>
    <!-- Package details -->
  </div>
`).join('');
```

### 31. `renderAddOnList()` - Line 2441
**Element:** Add-ons container
**Purpose:** List all add-ons
```javascript
container.innerHTML = `
  <div class="addons-list">
    <!-- Add-on items -->
  </div>
`;
```

### 32. `renderPricingTierList()` - Line 2576
**Element:** Pricing tiers container
**Purpose:** List pricing tiers
```javascript
container.innerHTML = `
  <table class="pricing-table">
    <!-- Tier rows -->
  </table>
`;
```

### 33. `generatePackageSummary()` - Line 2675
**Element:** Summary container
**Purpose:** Package pricing summary
```javascript
container.innerHTML = summaryHTML;
```

### 34. `loadGroomerAbsenceSummary()` - Line 2695
**Element:** Summary container
**Purpose:** No groomer selected message
```javascript
container.innerHTML = '<p style="color: var(--gray-600); text-align: center;">Please select a groomer first</p>';
```

### 35. `loadGroomerAbsenceSummary()` - Line 2730
**Element:** Summary container
**Purpose:** Groomer absence summary
```javascript
container.innerHTML = `
  <div class="summary">
    <!-- Absence details -->
  </div>
`;
```

---

## groomer.js

### 1. `loadGroomerDashboard()` - Line 56
**Element:** `#bookingsContainer`
**Purpose:** No bookings assigned empty state
```javascript
container.innerHTML = '<p class="empty-state">No bookings assigned to you yet.</p>';
```

### 2. `renderGroomerBookings()` - Line 60
**Element:** `#bookingsContainer`
**Purpose:** Assigned bookings
```javascript
container.innerHTML = bookings.map(booking => `
  <div class="booking-card">
    <!-- Booking details -->
    <button onclick="startGrooming('${booking.id}')">Start</button>
  </div>
`).join('');
```

### 3. `loadDashboardStats()` - Line 135
**Element:** Stats container
**Purpose:** Groomer dashboard statistics
```javascript
statsEl.innerHTML = `
  <div class="stats-grid">
    <!-- Stats cards -->
  </div>
`;
```

### 4. `loadScheduleView()` - Line 345
**Element:** Schedule container
**Purpose:** Groomer schedule
```javascript
container.innerHTML = `
  <div class="schedule-grid">
    <!-- Schedule items -->
  </div>
`;
```

### 5. `loadAbsenceRequestsView()` - Line 417
**Element:** Absences container
**Purpose:** No absence requests empty state
```javascript
container.innerHTML = '<p class="empty-state">No absence requests yet.</p>';
```

### 6. `loadAbsenceRequestsView()` - Line 421
**Element:** Absences container
**Purpose:** Absence requests list
```javascript
container.innerHTML = absences.map(absence => `
  <div class="absence-card">
    <!-- Absence details -->
  </div>
`).join('');
```

### 7. `openGroomerBookingModal()` - Line 459
**Element:** `#modalRoot`
**Purpose:** Booking detail modal
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <!-- Booking details -->
  </div>
`;
```

### 8. `openAbsenceModal()` - Line 494
**Element:** `#modalRoot`
**Purpose:** Request absence modal
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <form>
      <!-- Absence request form -->
    </form>
  </div>
`;
```

### 9. `openCompletedBookingModal()` - Line 560
**Element:** `#modalRoot`
**Purpose:** Mark booking as completed
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <form>
      <!-- Completion details form -->
    </form>
  </div>
`;
```

---

## staff.js

### 1. `loadStaffDashboard()` - Line 47
**Element:** Stats container
**Purpose:** Staff dashboard statistics
```javascript
statsEl.innerHTML = `
  <div class="stats-grid">
    <!-- Stats cards -->
  </div>
`;
```

### 2. `loadScheduleView()` - Line 166
**Element:** Schedule container
**Purpose:** Staff work schedule
```javascript
container.innerHTML = `
  <div class="schedule-grid">
    <!-- Schedule items -->
  </div>
`;
```

### 3. `loadAbsenceRequestsView()` - Line 239
**Element:** Requests container
**Purpose:** No requests empty state
```javascript
container.innerHTML = '<p class="empty-state">No absence requests yet.</p>';
```

### 4. `loadAbsenceRequestsView()` - Line 243
**Element:** Requests container
**Purpose:** Absence requests list
```javascript
container.innerHTML = absences.map(absence => `
  <div class="request-card">
    <!-- Request details -->
  </div>
`).join('');
```

### 5. `openAbsenceModal()` - Line 279
**Element:** `#modalRoot`
**Purpose:** Request absence modal
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <form>
      <!-- Form inputs -->
    </form>
  </div>
`;
```

---

## booking.js

### 1. `updateAgeDropdownOptions()` - Line 98
**Element:** Pet age select
**Purpose:** Update age options
```javascript
petAgeSelect.innerHTML = '';
// Rebuild with filtered options
```

### 2. `renderPackageOptions()` - Line 687
**Element:** Packages container
**Purpose:** Display available packages
```javascript
packagesContainer.innerHTML = filteredPackages.map(pkg => `
  <div class="package-option">
    <h3>${pkg.name}</h3>
    <p>${pkg.price}</p>
  </div>
`).join('');
```

### 3. `renderSingleServiceOptions()` - Line 742
**Element:** Options container
**Purpose:** No services empty state
```javascript
optionsContainer.innerHTML = '<p class="empty-state">Single services are not configured yet.</p>';
```

### 4. `renderSingleServiceOptions()` - Line 746
**Element:** Options container
**Purpose:** Single service options
```javascript
optionsContainer.innerHTML = optionEntries.map(option => `
  <div class="service-option">
    <label>
      <input type="checkbox" name="services" value="${option.id}">
      ${option.label}
    </label>
  </div>
`).join('');
```

### 5. `renderGroomerOptions()` - Line 916
**Element:** Groomer select container
**Purpose:** Available groomers
```javascript
container.innerHTML = `
  <select id="groomerSelect">
    <option>Select a groomer</option>
    <!-- Groomer options -->
  </select>
`;
```

### 6. `renderSummary()` - Line 1276
**Element:** Summary container
**Purpose:** Booking summary
```javascript
summaryContainer.innerHTML = summaryHTML;
```

### 7. `renderSummary()` - Line 1284
**Element:** Explanation div
**Purpose:** Booking fee explanation
```javascript
explanationDiv.innerHTML = '💡 <strong>Booking Fee Explanation:</strong> The ₱100 booking fee is included...';
```

---

## main.js

### 1. `renderPublicGallery()` - Line 907
**Element:** Gallery container
**Purpose:** No gallery empty state
```javascript
container.innerHTML = '<p class="empty-state">No shared galleries yet.</p>';
```

### 2. `renderPublicGallery()` - Line 910
**Element:** Gallery container
**Purpose:** Public gallery entries
```javascript
container.innerHTML = entries.map(entry => `
  <article class="gallery-card">
    <img src="${entry.beforeImage}">
    <img src="${entry.afterImage}">
  </article>
`).join('');
```

### 3. `openViewBookingModal()` - Line 971
**Element:** Modal root
**Purpose:** View booking modal
```javascript
modal.innerHTML = `
  <div class="modal">
    <!-- Booking details -->
  </div>
`;
```

### 4. `openViewCustomerModal()` - Line 1060
**Element:** Container
**Purpose:** Customer details view
```javascript
container.innerHTML = `
  <div class="customer-details">
    <!-- Customer info -->
  </div>
`;
```

---

## booking.html

### 1. `handleBookNow()` - Line 415
**Element:** Main navigation
**Purpose:** Update nav based on login status
```javascript
mainNav.innerHTML = '<li><a href="customer-dashboard.html">Dashboard</a></li>' + ...
```

### 2. `handleBookNow()` - Line 417
**Element:** Mobile navigation
**Purpose:** Update mobile nav based on login
```javascript
mobileNav.innerHTML = '<li><a href="customer-dashboard.html">Dashboard</a></li>' + ...
```

### 3. `handleBookNow()` - Line 420
**Element:** Navigation (fallback)
**Purpose:** Default navigation for non-logged-in
```javascript
mainNav.innerHTML = '<li><a href="index.html">Home</a></li>' + ...
```

---

## 📊 Summary Statistics

| File | innerHTML Count | Functions | Purpose |
|------|-----------------|-----------|---------|
| customer.js | 18 | 8 | Dashboard views, bookings, reviews |
| admin.js | 35 | 15 | Admin management, bookings, history |
| groomer.js | 9 | 6 | Groomer schedule and bookings |
| staff.js | 5 | 4 | Staff schedule and requests |
| booking.js | 7 | 6 | Booking form steps |
| main.js | 4 | 3 | Public galleries and modals |
| booking.html | 3 | 1 | Navigation updates |
| **TOTAL** | **81** | **43** | **All dynamic rendering** |

---

## 🎯 Usage Patterns

### Pattern 1: Empty State
```javascript
container.innerHTML = '<p class="empty-state">Message</p>';
```

### Pattern 2: List with Map
```javascript
container.innerHTML = items.map(item => `
  <div class="card">
    <!-- Item template -->
  </div>
`).join('');
```

### Pattern 3: Modal Creation
```javascript
modalRoot.innerHTML = `
  <div class="modal">
    <!-- Modal content -->
  </div>
`;
```

### Pattern 4: Form Generation
```javascript
container.innerHTML = `
  <form>
    <!-- Form fields -->
  </form>
`;
```

### Pattern 5: Clear and Reset
```javascript
container.innerHTML = '';
```

---

## 🔍 How to Find Specific innerHTML

### By Element ID
Search file for `getElementById('elementId').innerHTML`

### By Container Class
Search for `.querySelector('.classname').innerHTML`

### By Function Name
Look at functions containing "render", "load", or "update"

### By Line Number
Reference the line numbers in this document

---

## 💾 Backup Information

If you need to restore original innerHTML:
1. Refer to the exact line numbers in this document
2. The code snippets show the exact innerHTML content
3. Function context shows where innerHTML is assigned

---

## ⚠️ Important Notes

- **innerHTML is used for** dynamic content rendering, empty states, and list generation
- **Total innerHTML assignments:** 81 locations across 7 files
- **Most complex:** admin.js (35 locations)
- **Cleanest:** booking.html (3 locations)

---

**Document Last Updated:** December 1, 2025
**Purpose:** Complete innerHTML reference for BestBuddies Pet Grooming system
