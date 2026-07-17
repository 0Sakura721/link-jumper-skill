# link-jumper Test Cases / 测试用例

Scenarios: A(URL Jumping) B(Search Jumping) C(Stream Extraction) D(Error/Edge)

---

## A - URL Jumping

TC-A1: https://www.bilibili.com/video/BV1GJ411x7h7 -> AI uses ACTION_VIEW Intent

TC-A2: mailto:test@example.com -> AI opens email client

---

## B - Search Jumping

TC-B1: "search on B站 xxx" or "在B站搜索xxx" -> AI searches, jumps

TC-B2: "search GitHub transformers" -> AI searches GitHub, jumps

---

## C - Stream Extraction

TC-C1: play B站 video link -> AI extracts stream, plays

---

## D - Error/Edge

TC-D1: ftp link -> AI informs user

TC-D2: "play Netflix video" -> AI falls back to URL Jumping (DRM)
