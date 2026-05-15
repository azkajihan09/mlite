# Requirements Document

## Introduction

Redesign the "Detail Pasien" (Patient Detail) page in the mLITE healthcare management system (SIMRS) to provide a modern, clean, and user-friendly interface for doctors managing outpatient (rawat jalan) workflows. The redesign focuses on improving visual hierarchy, readability, and navigation efficiency while maintaining all existing functionality within the Bootstrap 3 + jQuery technology stack.

## Glossary

- **Detail_Pasien_Page**: The patient detail view displayed after a doctor selects a patient from the outpatient list, containing patient identity header and tabbed service sections
- **Patient_Header**: The top section of the Detail Pasien page displaying patient identity information (name, RM number, visit number, birth date, age, payment method, phone number)
- **Tab_Navigation**: The horizontal navigation component allowing doctors to switch between different service sections (Riwayat, Pemeriksaan, Resep, Resume Medis, etc.)
- **Riwayat_Tab**: The history tab displaying a table of past patient visits with clinical summaries
- **SOAP_Form**: The Subjective-Objective-Assessment-Plan form used by doctors to record clinical examinations
- **Rincian_Panel**: The tabbed detail panel showing prescriptions, procedures, lab requests, and radiology requests for a specific visit
- **Doctor_User**: A physician using the mLITE system to manage outpatient consultations
- **DataTables_Component**: The jQuery DataTables plugin used for rendering sortable, searchable patient data tables

## Requirements

### Requirement 1: Modern Patient Header Design

**User Story:** As a Doctor_User, I want a visually distinct and well-organized patient identity header, so that I can quickly identify the patient and their key information at a glance.

#### Acceptance Criteria

1. WHEN a patient is selected from the outpatient list, THE Patient_Header SHALL display patient identity information using a colored background (green gradient) with text that maintains a minimum contrast ratio of 4.5:1 against the background
2. THE Patient_Header SHALL organize patient data into a structured grid layout with labeled fields for: nama pasien, nomor RM, nomor kunjungan, tanggal lahir, umur, cara bayar, nomor telepon, and nomor registrasi SITB
3. THE Patient_Header SHALL use a card-based container with rounded corners (border-radius of 4px or greater) and box-shadow for visual elevation consistent with the Detail_Pasien_Page panel styling
4. WHILE the Doctor_User navigates between tabs on the Detail_Pasien_Page, THE Patient_Header SHALL remain rendered at the top of the page without being hidden or removed from the visible area
5. IF the patient data fields contain empty values (null, empty string, or whitespace-only), THEN THE Patient_Header SHALL display a dash character ("-") as placeholder for that field
6. IF the patient data fails to load after selection from the outpatient list, THEN THE Patient_Header SHALL display an error message indicating the data could not be retrieved and retain the patient's name and nomor RM if previously available

### Requirement 2: Modern Tab Navigation

**User Story:** As a Doctor_User, I want a clean and visually appealing tab navigation, so that I can easily switch between different service sections without confusion.

#### Acceptance Criteria

1. THE Tab_Navigation SHALL use a horizontal tab bar with colored active-tab indicators (bottom border highlight of 3px)
2. THE Tab_Navigation SHALL display tab labels in uppercase with consistent font weight (600 for inactive, 700 for active)
3. WHEN a tab is clicked, THE Tab_Navigation SHALL switch the visible content panel with a CSS transition of 0.2s duration and update the active indicator without triggering a page reload
4. WHILE the viewport width is less than 768px, THE Tab_Navigation SHALL enable horizontal scrolling (overflow-x: auto) to accommodate all tab items without wrapping
5. THE Tab_Navigation SHALL use distinct visual styling (color differentiation) for special tabs Permintaan Lab and Permintaan Rad, rendering their active-tab indicator and label in a different color from the standard tabs
6. WHILE the Detail_Pasien_Page is displayed, THE Tab_Navigation SHALL maintain the last active tab state until the doctor selects a different patient or performs a full page reload
7. WHEN the Detail_Pasien_Page is first loaded for a patient, THE Tab_Navigation SHALL set the first tab (Riwayat) as the default active tab and display its corresponding content panel
8. THE Tab_Navigation SHALL support keyboard navigation using arrow keys to move focus between tabs and Enter or Space key to activate the focused tab

### Requirement 3: Modernized History Table (Riwayat Tab)

**User Story:** As a Doctor_User, I want a clean and readable history table, so that I can quickly review a patient's past visits and clinical summaries.

#### Acceptance Criteria

1. THE Riwayat_Tab SHALL display visit history in a table with alternating row backgrounds (zebra striping) for improved readability
2. THE Riwayat_Tab SHALL use a light-colored table header (background #f5f5f5 or similar) with bold column labels
3. THE Riwayat_Tab SHALL display columns for: Tanggal, No. Rawat, Poli/Ruang/Dokter, Resume (Keluhan Utama, Diagnosa Utama, Jalannya Penyakit, Terapi/Catatan Dokter), Laboratorium, Radiologi, and Riwayat Intern
4. WHEN a history row contains clinical resume data, THE Riwayat_Tab SHALL format the resume content with labeled sub-sections using subtle typography differentiation (bold labels, normal-weight values)
5. THE Riwayat_Tab SHALL integrate with the DataTables_Component for sorting, searching, and pagination functionality with a default page size of 10 records and default sort by date descending
6. IF no history records exist for the patient, THEN THE Riwayat_Tab SHALL display an empty state message indicating no records are available
7. IF a history row contains partial resume data (some fields empty), THEN THE Riwayat_Tab SHALL display only the available fields without showing empty labels

### Requirement 4: Modernized SOAP Form Layout

**User Story:** As a Doctor_User, I want a clean and well-spaced examination form, so that I can efficiently fill in clinical data without visual clutter.

#### Acceptance Criteria

1. THE SOAP_Form SHALL use card-based containers with subtle borders (1px solid #e3e3e3) and a neutral light background (#ffffff or #fafafa) for form sections
2. THE SOAP_Form SHALL organize vital signs (tensi, suhu, nadi, RR, tinggi, berat) in a responsive grid with consistent spacing (minimum 12px gap between fields) using equal-width columns
3. WHILE the viewport width is 768px or greater, THE SOAP_Form SHALL display SOAP textarea fields (Subyektif, Obyektif, Assesment, Plan) in a 2-column layout with a minimum textarea height of 2 rows
4. WHILE the viewport width is less than 768px, THE SOAP_Form SHALL display SOAP textarea fields (Subyektif, Obyektif, Assesment, Plan) in a single-column layout
5. THE SOAP_Form SHALL use action buttons with consistent border-radius (3px), color coding (primary for save, danger for ICD, info for e-resep, success for complete), and a Font Awesome icon prefix on each button
6. WHEN the SOAP_Form is displayed, THE SOAP_Form SHALL pre-fill the date field with the current date in "YYYY-MM-DD" format and the time field with the current time in "HH:mm:ss" format
7. WHEN a Doctor_User focuses on an input or textarea field, THE SOAP_Form SHALL change the field border color to a distinct highlight color to indicate the active field
8. IF the SOAP_Form save action fails due to a network or server error, THEN THE SOAP_Form SHALL display an error notification message indicating the failure without clearing the entered form data

### Requirement 5: Modernized Rincian Panel (Prescriptions, Procedures, Lab, Radiology)

**User Story:** As a Doctor_User, I want a well-organized detail panel for prescriptions and requests, so that I can manage patient services efficiently.

#### Acceptance Criteria

1. THE Rincian_Panel SHALL use the same modern tab navigation style as the main Tab_Navigation with a 3px bottom-border active indicator, uppercase labels with font-weight 600 (inactive) and 700 (active), and distinct color styling for Permintaan Lab and Permintaan Rad tabs
2. THE Rincian_Panel SHALL display data tables with consistent styling: light header background (#f5f5f5), minimum 8px cell padding, 1px solid border (#f0f0f0) between rows, and 12px font size for table content
3. WHEN prescription data includes both racikan (compound) and non-racikan items, THE Rincian_Panel SHALL visually separate them with distinct section headers (h5 elements with font-weight 600 and minimum 12px top margin) labeled "Non Racikan" and "Racikan"
4. THE Rincian_Panel SHALL use compact action buttons (btn-xs with border-radius 2px, padding 4px 8px, font-size 11px) with danger color for delete/remove operations and success color for detail/view operations
5. THE Rincian_Panel SHALL apply the same zebra-striping pattern as the Riwayat_Tab (alternating row backgrounds using table-striped) for table rows
6. IF a tab section (Resep Dokter, Data Resep, Tindakan, Permintaan Lab, or Permintaan Rad) contains no records, THEN THE Rincian_Panel SHALL display the table structure with an empty tbody and no error message
7. WHEN a Doctor_User clicks a delete button on a record that has not been processed, THE Rincian_Panel SHALL display a confirmation dialog before executing the deletion and refresh the panel content upon successful deletion
8. IF a record has already been processed (e.g., prescription dispensed or lab sample taken), THEN THE Rincian_Panel SHALL disable the delete button for that record to prevent removal

### Requirement 6: Consistent Typography and Spacing

**User Story:** As a Doctor_User, I want consistent visual styling across all sections of the patient detail page, so that the interface feels cohesive and professional.

#### Acceptance Criteria

1. THE Detail_Pasien_Page SHALL use a base font size of 13px for body text and 15px for section headings (h4 elements)
2. THE Detail_Pasien_Page SHALL apply consistent vertical spacing of 20px margin-bottom for panels and 16px margin-bottom for form groups
3. THE Detail_Pasien_Page SHALL use a neutral color palette: #fafafa for panel body backgrounds, #f5f5f5 for table headers, #333 for heading text, and #555 for body text
4. THE Detail_Pasien_Page SHALL apply box-shadow (0 1px 3px rgba(0,0,0,0.08)) to all card/panel elements for subtle depth
5. THE Detail_Pasien_Page SHALL use the existing Bootstrap 3 grid system for responsive layout without introducing additional CSS frameworks

### Requirement 7: Responsive Behavior

**User Story:** As a Doctor_User, I want the patient detail page to work well on different screen sizes, so that I can use it on various devices in the clinic.

#### Acceptance Criteria

1. WHILE the viewport width is less than 768px, THE Detail_Pasien_Page SHALL stack the Patient_Header fields vertically in a single-column layout instead of in a grid
2. WHILE the viewport width is less than 768px, THE Tab_Navigation SHALL enable horizontal scrolling with overflow-x auto and hide the scrollbar visually on touch devices
3. WHILE the viewport width is less than 768px, THE SOAP_Form SHALL display textarea fields in a single-column layout with each textarea occupying full container width
4. THE Detail_Pasien_Page SHALL ensure no horizontal scrollbar appears on the page body at any viewport width from 320px to 1920px, all text remains readable without zooming, and all interactive elements remain visible without being clipped or overlapping
5. THE Detail_Pasien_Page SHALL use Bootstrap 3 responsive utility classes (col-md, col-sm, col-xs) for layout adaptation
6. WHILE the viewport width is less than 768px, THE Detail_Pasien_Page SHALL ensure all interactive elements (buttons, tabs, links) have a minimum touch target size of 44x44 CSS pixels
7. WHILE the viewport width is less than 768px, THE Riwayat_Tab and Rincian_Panel data tables SHALL enable horizontal scrolling within their container to prevent table content from overflowing the viewport

### Requirement 8: Visual Feedback and Interaction States

**User Story:** As a Doctor_User, I want clear visual feedback when interacting with the interface, so that I know which elements are active or clickable.

#### Acceptance Criteria

1. WHEN a Doctor_User hovers over a clickable table row, THE Detail_Pasien_Page SHALL highlight the row with a background color change to #f9f9f9 and display a pointer cursor
2. WHEN a Doctor_User hovers over a button, THE Detail_Pasien_Page SHALL apply a CSS transition of 0.2s duration for background and color property changes
3. WHEN a Doctor_User clicks a tab, THE Tab_Navigation SHALL update the active indicator within 100ms without triggering a full page reload
4. THE Detail_Pasien_Page SHALL use CSS transitions (transition: all 0.2s ease) for interactive state changes on buttons, links, and tabs
5. IF a form submission is in progress, THEN THE Detail_Pasien_Page SHALL disable the submit button and display a spinner icon until the server responds or 30 seconds have elapsed, whichever comes first
6. IF a form submission completes successfully, THEN THE Detail_Pasien_Page SHALL re-enable the submit button, remove the spinner icon, and display a success notification for 3 seconds
7. IF a form submission fails or the 30-second timeout is reached, THEN THE Detail_Pasien_Page SHALL re-enable the submit button, remove the spinner icon, and display an error notification indicating the submission was unsuccessful
