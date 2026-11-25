# Dasai Mochi – Website giới thiệu và hướng dẫn tự làm

Website một trang (single-page), song ngữ **Tiếng Việt / English**, giới thiệu robot mochi để bàn có biểu cảm (bản tự chế dùng **ESP32-C3 + màn OLED**) và hướng dẫn người mới từ đầu: chuẩn bị linh kiện, đấu dây, nạp firmware, cấu hình, kết nối điện thoại.

> **Lưu ý:** Đây là trang hướng dẫn độc lập của cộng đồng, **không phải trang chính thức** của dự án The Mochi. Firmware, công cụ nạp và trang thiết lập thuộc về tác giả gốc (xem phần [Ghi công](#ghi-công-và-bản-quyền)).

---

## Mục lục

- [Tính năng của website](#tính-năng-của-website)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Chạy thử trên máy](#chạy-thử-trên-máy)
- [Triển khai (deploy)](#triển-khai-deploy)
- [Hình ảnh cần chuẩn bị](#hình-ảnh-cần-chuẩn-bị)
- [Tuỳ chỉnh](#tuỳ-chỉnh)
- [Công nghệ và nguyên tắc thiết kế](#công-nghệ-và-nguyên-tắc-thiết-kế)
- [Nội dung các phần](#nội-dung-các-phần)
- [Ghi công và bản quyền](#ghi-công-và-bản-quyền)
- [English summary](#english-summary)

---

## Tính năng của website

- **Đa ngôn ngữ VI/EN:** chuyển ngay không cần tải lại trang, nhớ lựa chọn bằng `localStorage`, mặc định theo ngôn ngữ trình duyệt.
- **Khung màn hình OLED giả:** đôi mắt pixel tự chớp, tự đổi biểu cảm, bấm vào để đổi, có nút "Âm bản".
- **Trình chọn linh kiện:** tick những gì bạn muốn dùng (pin, buzzer, loa, cảm biến chạm, thẻ nhớ), trang gợi ý danh sách mua và sơ đồ đấu nối phù hợp.
- **Checklist tiến độ:** tick từng bước hướng dẫn, có thanh tiến độ, lưu trong `localStorage`.
- **Sơ đồ đấu nối dạng tab:** 6 tab từ cơ bản đến đầy đủ, điều khiển bằng bàn phím, ảnh phóng to (lightbox), bảng chân nối dạng chữ và nút sao chép.
- **FAQ / xử lý lỗi** dạng accordion.
- **Sáng / tối:** theo `prefers-color-scheme` hoặc nút đổi chế độ.
- **Trợ năng:** skip link, `focus-visible`, vùng chạm ≥ 44px, `aria` đầy đủ, tôn trọng `prefers-reduced-motion`.
- **Không phụ thuộc thư viện:** chỉ HTML, CSS, JavaScript thuần (ngoài Google Fonts).

---

## Cấu trúc thư mục

```
.
├── index.html        # Toàn bộ HTML + CSS + JS (inline)
├── README.md
└── images/           # Hình ảnh (xem danh sách bên dưới)
    ├── logo.png
    ├── favicon.png
    ├── hero-mochi.jpg
    ├── product-1.jpg … product-3.jpg
    ├── wiring-0-basic.png
    ├── wiring-1-battery.png
    ├── wiring-2-touch-buzzer.png
    ├── wiring-3-full-buzzer.png
    ├── wiring-4-full-amp.jpg
    ├── wiring-5-full-sd.jpg
    ├── chronos-1.png … chronos-12.png
    ├── sd-card-1.png
    └── sd-card-2.png
```

---

## Chạy thử trên máy

**Cách 1: mở trực tiếp.** Nhấp đúp `index.html` để mở bằng trình duyệt.

**Cách 2: dùng server cục bộ** (khuyến nghị, tránh một số hạn chế của trình duyệt với file local):

```bash
# Python 3
python -m http.server 8000
# rồi mở http://localhost:8000
```

Hoặc dùng tiện ích **Live Server** trong VS Code.

---

## Triển khai (deploy)

Vì là site tĩnh nên có thể đưa lên bất kỳ dịch vụ hosting tĩnh nào:

| Dịch vụ | Cách làm nhanh |
|---|---|
| **GitHub Pages** | Đẩy lên repo → Settings → Pages → chọn nhánh `main`, thư mục gốc |
| **Netlify** | Kéo thả thư mục dự án vào trang Netlify Drop |
| **Cloudflare Pages / Vercel** | Kết nối repo, để trống lệnh build, thư mục xuất là `/` |

Không cần bước build.

---

## Hình ảnh cần chuẩn bị

Đặt toàn bộ trong thư mục `images/` với **đúng tên file** dưới đây. Ảnh nào thiếu, trang sẽ hiển thị khung giữ chỗ (placeholder) ghi tên file cần có, giao diện không bị vỡ.

| File | Dùng ở đâu |
|---|---|
| `logo.png`, `favicon.png` | Thanh điều hướng, tab trình duyệt |
| `hero-mochi.jpg` | Hero (nếu không có sẽ dùng khung OLED giả) |
| `product-1.jpg` … `product-3.jpg` | Thư viện ảnh sản phẩm ở phần Giới thiệu |
| `wiring-0-basic.png` | Sơ đồ tab 1: ESP32-C3 + OLED |
| `wiring-1-battery.png` | Sơ đồ tab 2: pin + TP4056 |
| `wiring-2-touch-buzzer.png` | Sơ đồ tab 3: cảm biến chạm + buzzer |
| `wiring-3-full-buzzer.png` | Sơ đồ tab 4: tổng hợp dùng buzzer |
| `wiring-4-full-amp.jpg` | Sơ đồ tab 5: loa + MAX98357 |
| `wiring-5-full-sd.jpg` | Sơ đồ tab 6: loa + khuếch đại + microSD |
| `chronos-1.png` … `chronos-12.png` | Ảnh chụp màn hình Chronos theo thứ tự các bước (không dùng số 10) |
| `sd-card-1.png` | Cấu trúc thư mục thẻ nhớ |
| `sd-card-2.png` | Danh sách chủ đề GIF trong trang thiết lập |

**Ảnh Chronos theo bước:** 1 cài đặt · 2 tìm kiếm · 3 chọn thiết bị · 4 cấp quyền thông báo · 5 bỏ qua thiết lập · 6 Trình quản lý ESP32 · 7 bật Điều hướng · 8 bật gọi/tin nhắn · 9 chọn ứng dụng · 11 biểu tượng thông báo · 12 tự kiểm tra.

**Quy tắc ảnh:** luôn có `alt` (đa ngôn ngữ), có `width`/`height` để tránh nhảy layout, `loading="lazy"` (trừ ảnh hero).

> Chỉ dùng ảnh bạn có quyền sử dụng. Với sơ đồ và ảnh chụp từ trang gốc hoặc từ thành viên cộng đồng, hãy **xin phép** hoặc tự vẽ/chụp lại.

---

## Tuỳ chỉnh

### Đổi màu

Các màu nằm trong CSS variables ở `:root` (và bản tối trong `prefers-color-scheme: dark`):

```css
:root {
  --ink:  #14183A;  /* xanh mực – màu chủ đạo 1 */
  --cream:#FFF4E0;  /* kem sữa – màu chủ đạo 2 */
  /* màu phụ: hồng, bạc hà, đào, vàng chanh, lavender, xanh trời, matcha, san hô */
}
```

Nguyên tắc: **màu chủ đạo hẹp, màu phụ rộng**. Mỗi nhóm nội dung dùng một màu phụ riêng. Khi đổi màu, hãy kiểm tra tương phản chữ đạt tối thiểu **4.5:1** (WCAG AA).

### Sửa nội dung và thêm ngôn ngữ

Mọi chữ hiển thị nằm trong đối tượng `I18N` ở đầu phần JavaScript:

```js
const I18N = {
  vi: { "hero.title": "…", /* … */ },
  en: { "hero.title": "…", /* … */ },
};
```

- Gắn chữ vào HTML bằng `data-i18n="khoa"`; `alt` ảnh dùng `data-i18n-alt`, `aria-label` dùng `data-i18n-aria`.
- **Thêm ngôn ngữ mới:** thêm một khối (ví dụ `ja: {…}`) với đầy đủ khoá như `vi`, rồi thêm lựa chọn vào nút chuyển ngôn ngữ.
- Khoá nào thiếu ở ngôn ngữ mới sẽ không có chữ hiển thị, vì vậy nên sao chép từ `en` rồi dịch.

### Cập nhật link ngoài

Các link tới công cụ nạp firmware, trang thiết lập, GIF Maker, nhóm Facebook nằm ở phần cấu hình đầu file để dễ sửa:

| Mục | Địa chỉ |
|---|---|
| Công cụ nạp firmware | https://themochi.huykhong.com/ |
| Trang thiết lập | https://themochi.huykhong.com/thietlap |
| GIF Maker | https://themochi.huykhong.com/gif.html |
| Nhóm Facebook | https://www.facebook.com/groups/2442849046100292 |

---

## Công nghệ và nguyên tắc thiết kế

- **Công nghệ:** HTML5 ngữ nghĩa, CSS (Grid/Flex, CSS variables, `clamp()`), JavaScript thuần, SVG inline, Canvas/SVG cho khung OLED.
- **Chữ:** font tiêu đề serif có cá tính (Fraunces) + font nội dung dễ đọc (Be Vietnam Pro), nạp subset `vietnamese` và `latin-ext`, `font-display: swap`, có fallback `system-ui` / `Georgia`.
- **Họa tiết:** chủ đề pixel / chấm điểm OLED làm khung viền và đường ngăn cách section.
- **Khối giao diện:** bo góc lớn, viền dày, đổ bóng cứng kiểu sticker.
- **Hero:** một CTA chính ("Bắt đầu tự làm"), không dùng carousel.
- **Mobile-first:** chạy tốt từ 360px đến desktop; Chrome, Edge, Safari, Firefox.

---

## Nội dung các phần

Thứ tự section: Hero → Giới thiệu → **01** Chức năng → **02** Cần chuẩn bị gì → **03** Sơ đồ đấu nối → **04** Nạp firmware → **05** Cấu hình → **06** Kết nối điện thoại (Chronos) → **07** Nâng cao (GIF, thẻ nhớ) → FAQ → Cộng đồng và ghi công → Footer.

### Lưu ý kỹ thuật quan trọng (có trên trang)

- Ngoài VCC và GND, các chân khác có thể đổi trong trang thiết lập. **Tuyệt đối không dùng GPIO0.**
- Sơ đồ cơ bản: OLED `VCC→3.3V`, `GND→GND`, `SCL→GPIO 21`, `SDA→GPIO 20`.
- Dùng cáp USB Type-C **có truyền dữ liệu** (nhiều cáp chỉ sạc).
- Nạp firmware bằng **Chrome hoặc Edge** (cần Web Serial API); giữ nút **BOOT** khi cắm cáp.
- Sau khi nạp xong, **đóng trang nạp** trước khi mở trang thiết lập để không chiếm cổng COM.
- Phải bấm **"Lưu thiết lập"**, nếu không cấu hình sẽ mất sau khi reset.
- Thông báo và dẫn đường qua Chronos **chỉ hỗ trợ Android**.
- Chỉ tick **"Dùng thẻ nhớ"** khi đã cắm thẻ, nếu không thiết bị có thể bị treo.

### Những điểm cần kiểm tra trước khi đăng

- **Buzzer 5V hay 3.3V:** trang gốc ghi buzzer "5V" trong danh sách linh kiện nhưng sơ đồ nối vào 3.3V. Trang này làm theo sơ đồ gốc kèm ghi chú nhắc kiểm tra thông số buzzer của bạn.
- **Bảng chân nối tab 4–6:** các sơ đồ tổng hợp (buzzer, MAX98357, microSD) chỉ đối chiếu được từ ảnh gốc. Hãy tự kiểm tra và điền số GPIO chính xác trước khi công bố; không đoán số chân.

---

## Ghi công và bản quyền

- **The Mochi (firmware, công cụ nạp, trang thiết lập, GIF Maker):** do **Huykhong** phát triển, xem https://themochi.huykhong.com/
- **ChronosESP / ứng dụng Chronos:** tác giả **fbiego**.
- **Sơ đồ đấu nối tổng hợp:** bạn **Văn Hưng** (mạch 4.1, 4.2) và bạn **Nhân Data** (mạch 5).
- **Cộng đồng:** nhóm Facebook "Nạn nhân của Dasai Mochi", https://www.facebook.com/groups/2442849046100292
- Dự án này **không lưu hoặc phân phối firmware**; mọi liên kết nạp firmware trỏ về trang chính thức của tác giả.
- Nội dung hướng dẫn trong repo được viết lại bằng lời riêng dựa trên tài liệu công khai của dự án. Nếu dùng lại hình ảnh của người khác, hãy ghi nguồn và xin phép.

### Giấy phép

> Chưa chọn. Hãy thêm file `LICENSE` phù hợp cho **phần mã và nội dung do bạn tự viết** (ví dụ MIT cho mã, CC BY 4.0 cho nội dung). Giấy phép này **không** áp dụng cho firmware, hình ảnh hay tài liệu của bên thứ ba.

---

## English summary

A bilingual (Vietnamese / English) single-page website that introduces the **Dasai Mochi** desk robot (a DIY clone built on **ESP32-C3 + OLED**) and walks beginners through the full build: parts list, wiring diagrams, flashing firmware from the browser, configuration, phone integration (Chronos, Android only), and custom GIFs via microSD.

**Quick start:** put `index.html` next to an `images/` folder (see the file list above), then open it in a browser or run `python -m http.server 8000`.

**Highlights:** language switcher with `localStorage`, animated fake OLED screen, parts picker, progress checklist, tabbed wiring diagrams with lightbox, FAQ accordion, light/dark themes, accessibility-first, zero dependencies besides Google Fonts.

**Disclaimer:** this is an independent community guide, not the official The Mochi site. Firmware and tools belong to their original authors (Huykhong, fbiego); the guide links to the official sources rather than hosting any firmware.
