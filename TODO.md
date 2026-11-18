# Chalkbook website TODO

Reviewed 18 November 2026.
Baseline: `994f0595700258c1db5081e54429de654dfc7c88`. Publishing source: `merchant-ledger/site/`.

Website findings only. App implementation findings are tracked in the private app repository.

## W-01 [High] / Fix navigation for the GitHub Pages project path

All four pages use root-relative navigation. At /chalkbook/, Support resolves to /support.html rather than /chalkbook/support.html; Home, Privacy and Terms also leave the project. All four host-root destinations returned 404.

Suggested fix: Use base-path-safe relative links in the app's site/ source and publish them together. Add link checks that resolve URLs under the deployed project path.

Acceptance: From each page, every navigation destination returns the intended Chalkbook page with status 200.

Evidence: Reproduced in live browser and HTTP checks

[index.html:1](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/index.html#L1) | [support.html:1](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/support.html#L1) | [privacy.html:1](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/privacy.html#L1) | [terms.html:1](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/terms.html#L1)

- [ ] Implement and verify W-01.

## W-02 [Medium] / Replace the nonworking App Store call to action

The visible download link has href=APP_STORE_LINK. It navigates to a placeholder route, not an App Store listing. The nearby note says the listing is pending, but the link remains actionable.

Suggested fix: Use the approved App Store URL when available. Until then, show a clear non-link Coming soon state with a useful support or product-preview action.

Acceptance: No placeholder token remains in deployed HTML; the primary action either opens the verified listing or truthfully explains availability.

Evidence: Confirmed in source and rendered DOM; placeholder destination failed HTTP check

[index.html:16](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/index.html#L16)

- [ ] Implement and verify W-02.

## W-03 [Medium] / Increase link contrast in light mode

All pages use #00AA55 links. Their contrast against the light-mode white background is 3.052:1, below the 4.5:1 minimum for normal-size text. Dark mode measures 6.187:1 against #111111.

Suggested fix: Choose a darker light-mode link color, retain visible underlines and focus states, and check every state in both schemes. Keep the dark-mode color independently tuned.

Acceptance: Normal-size links meet 4.5:1 contrast and remain distinguishable on hover, focus and visited states.

Evidence: Calculated from source colors; dark-mode computed styles verified in browser

[index.html:1](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/index.html#L1) | [support.html:1](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/support.html#L1)

- [ ] Implement and verify W-03.

## W-04 [Medium] / Clarify what deletion does to separately saved copies

Support says deleting the app or using Delete all data removes everything, while the same site tells users to save encrypted backups in Files/iCloud Drive and export CSVs. Those external copies are not erased by deleting app records.

Suggested fix: Describe local deletion, other shops, Files/iCloud backups, CSV exports and recipient copies separately. Keep app and website wording consistent with verified deletion behavior.

Acceptance: A user can identify which copies remain and how to remove them; no blanket deletion promise contradicts the backup instructions.

Evidence: Confirmed website content inconsistency; app deletion trace reviewed

[support.html:6](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/support.html#L6) | [support.html:10](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/support.html#L10) | [privacy.html:23](https://github.com/frederickajay/chalkbook/blob/994f0595700258c1db5081e54429de654dfc7c88/privacy.html#L23)

- [ ] Implement and verify W-04.

## Before enabling invite links

- [ ] Serve AASA at the configured domain-root /.well-known/apple-app-site-association endpoint with the required headers and routes. Current project-path copies are templates for deferred accounts functionality, not an active integration.

## Website UX

- [ ] Add fictional screenshots and a short Gave/Got example.
- [ ] Put a verified download link or clear Coming soon state near the top.
- [ ] Explain Free versus Pro without ambiguous export wording.
- [ ] Add a main landmark, skip link and current-page navigation.
- [ ] Organize backup, restore, deletion and support into clear FAQ sections.
- [ ] Test narrow screens, keyboard focus, enlarged text and light/dark contrast.

## Publishing and verification

- [ ] Fix and retain this TODO in merchant-ledger/site/ before running publish_site.sh; the publisher uses rsync --delete.
- [ ] Add automated checks for project-base navigation, placeholders, contrast colors and valid matching association JSON.

Current evidence: four content pages returned 200, all four shared host-root navigation destinations returned 404, light-mode link contrast measured 3.052:1, and the download link is still a placeholder. No site fixes are included in this TODO commit.
