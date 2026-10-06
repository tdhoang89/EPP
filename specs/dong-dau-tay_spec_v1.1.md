# Đống dâu — Macro tiêu điểm — Equation Painting Spec v1.1

Bức Henry chọn trong tập duyệt `dong-dau-tay` (F, thẻ O), **bản đánh bóng v1.1** (thẻ OV2). Bản v1.0 được duyệt giữ nguyên ở `final/dong-dau-tay_spec_v1.md`. Một Công Thức, PHỎNG TÁC bậc 2.

## 0. Metadata

| Trường | Giá trị |
|---|---|
| Slug | `dong-dau-tay` — ứng viên F (`dong-dau-tay-macro`) |
| Ngày / phiên bản | 06/10/2026 — v1.1 (từ v1.0: dáng riêng từng quả, hạt bớt trật tự; mục 10) |
| Mục tiêu | PHỎNG TÁC bậc 2 (lấy palette, bố cục, vị trí–cỡ mảng lớn, hướng sáng; không lấy đường viền, texture) |
| Thesis | Ống macro khẩu lớn: quả giữa và vùng quanh nó nét, quả xa mềm dần (độ sâu trường ảnh bằng độ mềm biên và mất chi tiết), phản chiếu ở quả xa nở mềm, tối góc và hạt ảnh của máy ảnh; cược vào dấu hiệu quang học của ảnh chụp, chấp nhận lệch khỏi ảnh nguồn vốn nét toàn khung. v1.1 (đánh bóng): mỗi quả một dáng riêng và hạt bớt trật tự, để quả bớt vẻ dập cùng một khuôn khi xem ở 100%. |
| Vai / xếp hạng | Ảnh chụp — quang học / v1.0: hạng 1 trong 4 của lô ảnh chụp, Henry chọn; v1.1 thắng v1.0 trong so cặp mù của vòng đánh bóng |
| Họ công thức | `anh-chup (quang học)` |
| Trục | bố cục neo 1:1, tiêu điểm quả giữa · palette ĐO, quả xa trầm · PBR + bump + độ sâu trường ảnh + dáng riêng từng quả, hạt lệch · softbox, phản chiếu xa nở mềm · 21 quả + 14 đài lá, nét giảm dần · tả thực quang học · độ sâu trường ảnh, hạt ảnh |
| Nguồn | ảnh tham chiếu `input/dau-tay_ref.jpeg` (554 × 554, SHA-256 `c115eac6b613ef94f4ec4ecf47c4988a21080028284773f08c0341420b111828`) — đống dâu tây chín chất đầy khung |
| Xuất xứ & quyền của ảnh tham chiếu | chưa rõ (Henry không nói); spec không chứa pixel nào của ảnh tham chiếu |
| Độ phân giải chuẩn | 1108 × 1108 (A = 1), SS = 2 |
| COLOR_SPACE | linear cho chiếu sáng, mã hoá sRGB từng mẫu trước khi lấy trung bình SS (mục 2) |
| Kernel / kit | EP-KERNEL v1.1 + OF-KIT v1.1 |
| Hạng độ dài | LAI (Henry duyệt ở Checkpoint 1): 11489 ký tự, 663 hằng số, 207 dòng, 27 hàm phụ riêng, render chuẩn ≈ 42.3 s; một bảng neo 35 dòng (Q 21 + DL 14) |
| Môi trường render chuẩn | Python 3.14.3, numpy 2.4.6, Windows 11; render chuẩn ≈ 42.3 s |
| Tương đồng (thay Fidelity A) | `lum12` 0.634 (dải bậc 2 đã duyệt 0,30–0,85), ΔE palette 7.2 (≤ 10), `edge_corr` 0.175 (báo cáo, không dùng để loại), lệch phân bố sáng 0.060 → trong dải |
| Fidelity B | xem mục 6: cấp R1; probe, hash, POINTWISE, clean-room |
| Henry duyệt | ACCEPTED (06/10/2026) — Henry: "Ok Duyệt." (trả lời câu "chọn v1.0 hay v1.1"; hiểu là duyệt v1.1). v1.1 là bản chính; v1.0 giữ nguyên ở final/dong-dau-tay_spec_v1.md |

Ghi công:

> Khuôn "một hàm cho cả bức tranh" và cổng e^{−e^{u}} theo Hamid Naderi Yeganeh, *Pictures from Networks of Mathematical Functions*, Math Horizons 32(1), 2024. Công thức, bố cục và hình ảnh trong spec này là tác phẩm mới.
> The one-function frame (F(H₀), F(H₁), F(H₂)) and the gate e^{−e^{u}} follow Hamid Naderi Yeganeh, *Pictures from Networks of Mathematical Functions*, Math Horizons 32(1), 2024. The formulas, composition and image in this specification are new work.

## 1. Hướng dẫn tái tạo cho AI

### 1.1 Nếu bạn chạy được Python → Prompt A

```text
You are receiving an Equation Painting specification, not a request to imagine an image.
Reproduce the image EXACTLY.

1. First determine whether you can execute Python 3 with NumPy. If you cannot, reply
   EXECUTION_UNAVAILABLE and return the unchanged code block with the run instructions
   below. Do not substitute a generated illustration for a replay.
2. Copy the single Python code block in Section 5 verbatim into a file and run it. Do not
   edit, reinterpret, optimize, "fix", or restyle any formula, constant, convention, sampling,
   or layer order. Do not add or remove objects. Do not install or fetch anything silently;
   the script needs only Python 3 and NumPy and writes `<slug>_render.png` at W x H.
3. The script prints PASS/FAIL for every probe pixel in Section 6 (tolerance +/-2 per
   channel), the EP-PIX v1 pixel hash, and REPLAY OK or REPLAY MISMATCH.
4. Report: the rendered image, the probe and hash results, your Python and NumPy versions.
   A matching hash proves replay of this specification, not similarity to the original source.
5. If anything FAILS, do not adjust the image or the code. Report which probes failed and by
   how much, and your environment.

The equations are the complete specification of the image. Evaluate them literally.
```

Ghi chú môi trường (ngoài prompt): trên Windows chạy `python -X utf8 spec.py`.

### 1.2 Nếu bạn chỉ đọc được toán → Prompt B

```text
You are given a complete Equation Painting specification but cannot run the reference code.
Implement Sections 2-4 exactly in your language. The scene is a pure function of (x, y):

- Canvas W x H, SS samples per pixel edge. Sample (i, j) of pixel (m, n) has coordinates
  x = ((m + (i + 0.5)/SS)/W * 2 - 1) * A, y = 1 - (n + (j + 0.5)/SS)/H * 2, with A = W/H;
  y points up. Average the SS*SS samples (j outer, i inner) before clipping.
- Angles in radians; atan2 takes (y, x); rotate() as defined in Section 2.
- Colours are floats in [0, 1] in the declared COLOR_SPACE. Composite the layers in the listed
  order with the over/add/multiply/screen operators as defined. Clip once at the end, then
  quantize with floor(255 * v + 0.5).
- Masks: M = 1 - smoothstep(-EDGE, EDGE, sd) with EDGE as declared; SDFs are negative inside.
- Noise: the 32-bit integer hash in Section 2, bit-exact; floor toward minus infinity; no
  library random functions.
- Evaluate every pixel literally. Do not replace any object or texture with a drawing
  primitive, asset, filter, or blur.

Then check the probe pixels in Section 6 (tolerance +/-2 per channel) and compute the EP-PIX v1
hash (SHA-256 of the ASCII header "EP-PIX v1 W H RGB\n" followed by the RGB bytes, top row
first). Report PASS/FAIL per probe and whether the hash matches. If anything fails, report it;
do not alter the specification.
```

### 1.3 Nếu bạn là model sinh ảnh → Prompt C (bậc xấp xỉ)

```text
[APPROXIMATE_GENERATIVE_INTERPRETATION. This model cannot evaluate equations, so the result is
an approximation of the exact image defined in this specification. It must never be used to
update the specification's probes or hash.]

Create a flat, procedural, vector-like illustration with aspect ratio W:H, soft anti-aliased
edges, no text, no watermark. Follow the structured description in Section 7 exactly: render
the layers in the listed order, use the listed hex colours, place each element at the listed
position (percent of width from the left, percent of height from the top) with the listed size
(percent of image height) and rotation. Do not add elements that are not listed. Do not change
the colour palette.
```

### 1.4 Nếu bạn được yêu cầu sửa ảnh này → Prompt D

```text
You are receiving an Equation Painting specification and a change request. This is an edit of
the image program, not a replay.

Identify exactly which objects, parameters and dependent relations (shadows, reflections,
occlusion) the change affects. Change only those, in the single authoritative code block; keep
every other parameter, seed, layer order and convention unchanged. Render, verify the intended
effect, regenerate the probe table and pixel hash, bump the version, and deliver the new image
and the new self-contained specification. Never keep the old hash for a new image.
```

## 2. Quy ước

Mục này tự đủ; không cần bible.

- **Khung**: 1108 × 1108 pixel, A = W/H = 1, SS = 2 (2 × 2 mẫu mỗi pixel). Pixel (m, n): m là cột từ trái (0…1107), n là hàng từ trên (0…1107).
- **Toạ độ mẫu** (i, j) ∈ {0, 1}² của pixel (m, n): x = ((m + (i + 0,5)/2)/1108·2 − 1)·A, y = 1 − (n + (j + 0,5)/2)/1108·2. x, y ∈ [−1, 1], **y hướng lên**. Khoảng cách hai mẫu kề nhau PX = 2/(1108·2).
- **Màu pixel** = trung bình cộng 4 mẫu, cộng theo thứ tự j ngoài, i trong, **trước** khi clip.
- **Scene là hàm thuần**: scene(x, y, A, px) trả về bộ ba (H₀, H₁, H₂) (kênh R, G, B). Ảnh: (R, G, B) = (F(H₀), F(H₁), F(H₂)), với F(t) = ⌊255·clamp(t, 0, 1) + ½⌋ (làm tròn nửa lên, không dùng round của thư viện). Clip một lần ở cuối.
- **Số phức**: z = x + iy. Góc tính bằng radian, dương ngược chiều kim đồng hồ; arg w = atan2(Im w, Re w) (đối số thứ nhất là thành phần y); e^{iθ} = cos θ + i sin θ.
- **Màu**: số thực [0, 1]; không gian màu như mục "Không gian màu (lô ảnh chụp)" dưới đây.
- **Gộp lớp dạng đóng** fold_over: bắt đầu bằng nền Γ, với mỗi lớp (M, K) theo đúng thứ tự liệt kê: H_v ← H_v·(1 − M) + K_v·M. Lớp sau đè lớp trước. Tương đương H_v = Γ_v·Π(1 − M_k) + Σ_k M_k K_{k,v} Π_{j>k}(1 − M_j).
- **Bước mềm** S(δ) = ¼(1 − δ̂)²(2 + δ̂), δ̂ = clamp(δ, −1, 1); S(δ) = 1 khi δ ≤ −1, = 0 khi δ ≥ 1 (bằng 1 − smoothstep(−1, 1, δ)). Mặt nạ từ SDF: M = S(sd/EDGE), EDGE = 0,75·PX; SDF âm bên trong.
- **Hash số nguyên** hash2(i, j) → [0, 1), mọi phép tính mod 2³² (số âm đưa về mod 2³² trước): n = i·374761393 + j·668265263 + 2654435769; n ← n ⊕ (n ≫ 16); n ← n·0x7FEB352D; n ← n ⊕ (n ≫ 15); n ← n·0x846CA68B; n ← n ⊕ (n ≫ 16); hash = n/2³². Kiểm tra: hash2(0, 0) = 0,007765133399516344. Đối số là số thực có giá trị nguyên (kết quả của ⌊ ⌋). ⌊ ⌋ luôn là floor về −∞.
- **Worley F1** worley(x, y, f, seed): (ξ, η) = (x·f, y·f); với 9 ô (⌊ξ⌋ + di, ⌊η⌋ + dj), di, dj ∈ {−1, 0, 1}, hạt của ô (a, b) đặt tại (a + hash2(a + 7919·seed, b), b + hash2(b + 7919·seed, a + 1)); F1 = khoảng cách Euclid nhỏ nhất từ (ξ, η) tới 9 hạt (đơn vị ô).
- **Không có** blur, phép lân cận, ảnh, font, RNG thư viện; mọi lặp là vòng lặp hữu hạn theo chỉ số.
- **Tính theo ô**: code tham chiếu tính ảnh theo 8 × 8 ô và bỏ qua các lớp có mặt nạ bằng 0 tuyệt đối trong ô (biến VIEW, hàm near). Đây chỉ là cách tính nhanh: kết quả trùng từng bit với render_of toàn ảnh của OF-KIT (đã kiểm ở 1108 × 1108). Bản triển khai Tier 2 cứ tính mọi lớp ở mọi pixel.
- **Hash pixel EP-PIX v1** = SHA-256 của chuỗi ASCII `EP-PIX v1 1108 1108 RGB\n` nối với các byte RGB uint8 theo hàng từ trên xuống, cột từ trái sang. File ra: PNG 8-bit RGB không alpha.
- **Windows**: chạy `python -X utf8 <file>.py` (dòng in của OF-KIT có ký tự ngoài cp1252).
- **Không gian màu (lô ảnh chụp)**: COLOR_SPACE = linear cho chiếu sáng. Hằng số màu đo (sRGB) đổi sang tuyến tính bằng lin(c) (IEC 61966-2-1, mục 4.2) khi nạp; mọi lớp gộp trong tuyến tính; mỗi **mẫu** được phơi sáng, qua vai sáng `tone` rồi mã hoá sRGB bằng linear_to_srgb(l) = 12,92·l nếu l ≤ 0,0031308, ngược lại 1,055·l^{1/2,4} − 0,055 (l kẹp ≥ 0) **trước** khi lấy trung bình 4 mẫu. (Khác profile linear của tập I §5.3, vốn mã hoá sau khi lấy trung bình; ở đây mã hoá từng mẫu để scene vẫn là hàm thuần trả về màu cuối và Test A pointwise chạy được.)
- **Value noise** value_noise(x, y; f, seed) (hạt ảnh): (ξ, η) = (x·f, y·f); i₀ = ⌊ξ⌋ + 7919·seed, j₀ = ⌊η⌋; t_x = ξ − ⌊ξ⌋, t_y = η − ⌊η⌋; u = t²(3 − 2t) từng trục; nội suy song tuyến tính hash2(i₀, j₀), hash2(i₀ + 1, j₀), hash2(i₀, j₀ + 1), hash2(i₀ + 1, j₀ + 1).

## 3. Palette

| Tên | Hex | RGB float | Dùng ở | Cơ sở |
|---|---|---|---|---|
| K_S | `#6E1013` | (0.431, 0.061, 0.074) | đỏ tối (mặt quay đi, quả sau) | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_M | `#AF221B` | (0.686, 0.133, 0.106) | đỏ giữa | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_L | `#DF2212` | (0.875, 0.133, 0.071) | đỏ sáng (vai quả đón sáng) | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_GAP | `#2F0E09` | (0.184, 0.055, 0.035) | khe tối giữa các quả | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_HL | `#ECD3BD` | (0.925, 0.827, 0.741) | lấp lánh / bóng ướt | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_G1 | `#9CAD4F` | (0.612, 0.678, 0.310) | đài lá – sáng | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_G0 | `#6D6026` | (0.427, 0.376, 0.149) | đài lá – tối | ĐO (k-means Lab trên ảnh tham chiếu) |
| K_SEED | `#C9A553` | (0.788, 0.647, 0.325) | hạt (quả bế) | ĐO (k-means Lab trên ảnh tham chiếu) |

## 4. Định nghĩa toán học

### 4.1 Công thức phát triển (Level A, để đọc)

Như bản Studio, thêm quang học máy ảnh: quả tiêu điểm (quả lớn nhất ở giữa) và vùng bán kính 0,35 quanh nó nét; ra xa hơn, biên quả mềm dần, chi tiết hạt và hốc mất dần, phản chiếu nở mềm (độ sâu trường ảnh làm bằng độ mềm biên và độ chi tiết, không có blur). Tối góc ống kính và hạt ảnh đơn sắc. v1.1: mỗi quả có dáng riêng — dáng chung dãn theo bán kính bằng ba số hạng Fourier bậc thấp (vai/chóp, méo bậc 2 và 3; độ lệch lớn nhất của mép 3,9–8,5% bán kính, trung vị 5,8%) lấy từ hash của sid; hạt bớt trật tự — mỗi hạt lệch nhẹ khỏi nút lưới, hốc to nhỏ và sâu nông khác nhau, hạt vàng to nhỏ theo hốc, điều khiển bằng hai nhiễu giá trị trên mặt quả.

### 4.2 Công thức chuẩn (Level B)

(R, G, B)(m, n) = (F(H₀), F(H₁), F(H₂)), với (H₀, H₁, H₂) = trung bình 4 mẫu của scene tại các mẫu (i, j) của pixel (mục 2). Mọi hàm phụ dưới đây theo đúng thứ tự định nghĩa trong code; số trong ngoặc vuông là ID trong code. Ký hiệu dùng chung: L̂ = (L_x + iL_y)/|L_x + iL_y| (hướng sáng trong mặt ảnh, góc θ_L = arg L̂ ≈ 130°); Λ_z = L̂·e^{i(φ_i − α_i)} (hướng sáng trong hệ ζ của quả i); Λ_q = L̂·e^{−iα_i} (hướng sáng trong hệ q); τ̂ = e^{i(φ_i − π/2)} (hướng chóp trong hệ ζ).

- **[F-01] `_qc`** — c_i = x_i + i·y_i: tâm quả i lấy từ bảng neo Q (P-01).
- **[F-02] `_host`** — Quả chủ của đài lá k (tâm d_k = DLx_k + i·DLy_k): h(k) = max{i : |d_k − c_i| < r_i}; nếu tập rỗng, h(k) = argmin_i |d_k − c_i|/r_i.
- **[F-03] `_pose`** — Tư thế quả i (seed gắn với object qua sid_i = cột 4 của Q, tập I nguyên tắc 6). K_i = {k : h(k) = i}. Nếu K_i ≠ ∅: δ_i = c_i − d_{k*} với k* ∈ K_i làm |c_i − d_k| nhỏ nhất; β_i = arg δ_i; ε_i = clamp((|δ_i|/r_i − 0,15)/0,5, 0, 1). Nếu K_i = ∅: β_i = −π/2 + 0,7·cos(2,3·sid_i + 1), ε_i = 1 (CHỌN). Kết quả: R_i = RS·r_i, α_i = β_i + π/2, φ_i = 1,7·sid_i. Thứ tự lớp SEQ: quả 0, các đài lá có h(k) = 0 (k tăng), quả 1, …, quả 20, các đài lá có h(k) = 20.
- **[F-04] `berry`** — Dáng dâu (O01): ω = (z − c_i)·e^{−iα_i}/R_i, u = Re ω, v = Im ω (v > 0 về phía cuống), v⁺ = max(v, 0); q = u / max(1 + 0,36·ε_i·v, 0,3) + i·(v + 0,15·ε_i·(v⁺)²·e^{−6u²}) / (1 + 0,1·ε_i); sd_i = (|q| − 1)·0,85·R_i (SDF xấp xỉ, âm bên trong); n_w = q·e^{iα_i} (thành phần (x, y) của pháp tuyến trong hệ ảnh).
- **[F-05] `surf`** — Toạ độ trên mặt quả: ζ = q·(1 + 0,57·min(|q|², 1))·e^{iφ_i} (xấp xỉ arcsin τ/τ: lưới hạt dày lên ở mép).
- **[F-06] `pw`** — pw(t, n) = tⁿ với n ∈ {2, 4, 8, …}, tính bằng bình phương lặp (t ← t², n ← n/2).
- **[F-07] `hexlat`** — Lưới lục giác: T(ζ; a) = [cos(a·Re ζ) + cos(a·Re(ζ·ε₃)) + cos(a·Re(ζ/ε₃))]/3, ε₃ = e^{2πi/3}; T = 1 tại tâm hạt, nhỏ nhất −½.
- **[F-08] `near`** — Không thuộc định nghĩa ảnh. near(c, rad) = đúng nếu VIEW chưa đặt hoặc hình vuông tâm c nửa cạnh rad giao khung VIEW đang tính. Mỗi lớp được gọi kèm một rad mà ngoài |z − c| ≥ rad mặt nạ của lớp bằng 0 tuyệt đối, nên bỏ qua lớp không đổi ảnh.
- **[F-09] `lin`** — Đổi hằng số màu sRGB → tuyến tính: lin(c) = c/12,92 nếu c ≤ 0,04045, ngược lại ((c + 0,055)/1,055)^2,4. Albedo: ALB = lin(K_L)/1,05 ⊙ (1; 0,8; 0,8); ALB_SEED = lin(K_SEED), ALB_G1 = lin(K_G1), ALB_G0 = lin(K_G0), GAPL = lin(K_GAP), SL = lin(K_S). Trục softbox: UB = (−L_y, L_x, 0)/|(L_x, L_y)|, VB = L × UB; softbox phụ L₂ = BOX2D/‖BOX2D‖, UB₂, VB₂ tương tự; FL = FILLD/‖FILLD‖.
- **[F-10] `tone`** — Vai sáng: tone(x) = KNEE + (1 − KNEE)·(1 − e^{−(max(x, KNEE) − KNEE)/(1 − KNEE)}) + min(x, KNEE) − KNEE (= x khi x ≤ KNEE; cong mềm về 1 khi x > KNEE, trơn bậc 1).
- **[F-11] `encode`** — encode(H)_v = linear_to_srgb(tone(EXPO·H_v)) (mục 2).
- **[F-12] `unit3`** — unit3(x, y, z) = (x, y, z)/√(x² + y² + z² + 10⁻¹²).
- **[F-13] `spec`** — Phản xạ gương: R = (2n_z n_x, 2n_z n_y, 2n_z² − 1) (phản xạ của hướng nhìn V = (0, 0, 1)); a = R·UB, b = R·VB; box = S((|a| − BOXW)/e)·S((|b| − BOXH)/e)·clamp((R·L − 0,3)/0,3, 0, 1), e = BOXE (hoặc box_e nếu được truyền); box₂ tương tự với UB₂, VB₂, L₂, BOX2W, BOX2H; env = 0,06·ENV·(0,25 + 0,75·clamp(0,5 + 0,5·R_y, 0, 1)) + BOX2I·box₂; t = clamp(1 − n_z, 0, 1); fr = F0 + (1 − F0)·t⁵ (Fresnel Schlick); trả về (fr·(BOXI·box + env), box).
- **[F-14] `shade_flesh`** — Thịt quả: n·L; n_f = max(n·FL, 0); ao = (0,32 + 0,68·√n_z0)·(1 − PITD·P); body_v = alb_v·(KEY_v·clamp((n·L + WRAP_v)/(1 + WRAP_v), 0, 1) + FILLC_v·n_f + AMBI·(0,55 + 0,45·n_z))·ao (khuếch tán bọc theo kênh = tán xạ dưới bề mặt).
- **[F-15] `sepal`** — Đài lá k (O02), σ = sid của đài lá (cột 4 của DL): ρ = 1,75·s_k, m = 7 + (σ mod 3); w = (z − d_k)/ρ, r = |w|, ψ = arg w; a = (ψ + π)·m/(2π) + 0,37σ; j = ⌊a + ½⌋; e = a − j; j_m = j − m·⌊j/m⌋; Λ = 0,75 + 0,4·hash2(j_m + 31σ, 5) (dài từng cánh); w_j = 0,9 + 0,1·hash2(j_m + 13σ, 3) (rộng từng cánh, ≤ 1); p = max(1 − 2|e|/w_j, 0); sd = (r − (0,18 + (Λ − 0,18)·p^0,6))·0,45ρ; trả về sd, r, w, e/w_j, Λ.
- **[F-16] `pr_sepal_color`** — Màu cánh đài: t = clamp(r/Λ, 0, 1); θ = 0,05 + (1 − t)^1,5 (gốc nằm trên quả, ngọn cong lên); (c_x, c_y) = (Re w, Im w)/max(r, 10⁻⁹); n = unit3(sin θ·c_x − 0,9e·c_y, sin θ·c_y + 0,9e·c_x, cos θ) (gập dọc gân giữa); dry = 0,45·S((0,88 − t)/0,06); p_e = max(1 − 2|e|, 0); rim = 0,35·S((p_e − 0,22)/0,12) (mép sáng); vein = 0,3·S((0,93 − p_e)/0,03)·S((t − 0,85)/0,1) (gân tối); alb_v = ((ALB_G0 + (ALB_G1 − ALB_G0)(0,3 + 0,7t))_v·(1 − vein)(1 − rim) + 1,35·ALB_G1,v·rim)·(1 − dry) + 0,55·ALB_G0,v·dry; (sp, ·) = spec(n, 0,12); K_v = alb_v·(KEY_v·(max(n·L, 0) + 0,35·max(−n·L, 0)) + 0,5·FILLC_v + AMBI)·(0,6 + 0,4t) + 0,5·sp; cuống: st = S((r − 0,1)/0,025), sl = 0,55 + 0,225·clamp(1 + (Re w·Re L̂ + Im w·Im L̂)/0,1, 0, 2); K_v ← K_v·(1 − st) + 0,8·ALB_G1,v·(KEY_v·sl + AMBI)·st.
- **[F-17] `pr_ground`** — Khe: dome = clamp(1 − F1(Re z, Im z; 4,5; 3)/0,8, 0, 1)²; Γ_v = GAPL_v·(0,45 + 0,3·dome) + (SL_v − GAPL_v)·0,18·dome² (tuyến tính).
- **[F-18] `pr_layers`** — Lớp theo SEQ (BLACK = (0, 0, 0)): quả i — L02 bóng đổ (M = SHA·S(sd_i(z + SHD·L̂)/(0,3R_i)), K = BLACK), L03 bóng tiếp xúc (M = CONTA·clamp(1 − sd_i/(CONTW·R_i), 0, 1)², K = BLACK), L04 quả (M = S(sd_i/ed), K = berry_fn(z, i, ed)), ed = EDGE + edge_fn(0, i) (edge_fn = 0 nếu không có); đài lá k — L05 bóng (M = 0,5·S(sd_k(z + 0,03·L̂)/0,012), K = BLACK), L06 đài lá (M = S(sd_k/ed), K = pr_sepal_color), ed = EDGE + edge_fn(1, k). sd_i theo GEO (= berry_v ở v1.1: dáng riêng từng quả). Lớp quả bỏ qua được khi |z − c_i| ≥ RADK·R_i + SHD (mặt nạ bằng 0).
- **[F-19] `grain`** — Hạt ảnh: grain(x, y; amt, f = 520, seed = 99) = amt·(value_noise(x, y; f, seed) − ½), cộng sau khi mã hoá.
- **[F-20] `vignette`** — Tối góc: vignette(x, y; k) = 1 − k·(x² + y²)/2, nhân vào màu tuyến tính trước khi mã hoá.
- **[F-21] `_g`** — Quả tiêu điểm là quả có sid = FOCS (dòng FOCI); mức mất nét: g(c) = min(max(|c − c_FOCI| − SHARP, 0)/0,9, 1)^1,3; GB_i = g(c_i)·(0,75 + 0,25·(1 − r_i/0,337)) (quả nhỏ mờ thêm); GD_k = g(d_k).
- **[F-22] `_hc`** — hash2 cho hằng số, tính bằng số nguyên thuần (cùng bit với hash2 của mục 2).
- **[F-23] `_shape`** — Hệ số dáng của quả có sid s: h_k = hash2(s + 401, k), k = 0…4; b₁ = SHP·(1,6h₀ − 0,5) (vai phồng khi b₁ > 0, chóp phồng khi b₁ < 0); a₂ = SHP·(0,4 + 0,6h₁); f₂ = 2πh₂; a₃ = SHP·(0,15 + 0,35h₃); f₃ = 2πh₄. Bảng SHAPE_i = _shape(sid_i), i = 0…20 (theo sid, không theo dòng).
- **[F-24] `berry_v`** — Dáng riêng của quả i (O01, v1.1): (b₁, a₂, f₂, a₃, f₃) = SHAPE_i; θ = arg((z − c_i)·e^{−iα_i}) (góc trong khung quả, θ = π/2 về phía cuống); r(θ) = 1 + b₁·sin θ + a₂·cos(2θ + f₂) + a₃·cos(3θ + f₃); (sd′, q, n_w) = berry(c_i + (z − c_i)/r(θ), i); trả về (sd′·r(θ), q, n_w). Tức là dáng chung `berry` dãn theo bán kính r(θ) quanh tâm quả; q và n_w vẫn có |q| = 1 ở mép, nên bóng khối và lưới hạt trải theo dáng mới. GEO = berry_v.
- **[F-25] `bumped_v`** — Pháp tuyến có lỗ hạt (v1.1), σ = sid của quả: ζ′ = surf(q, φ); ζ₀ = ζ′ + WARP·(cos(11·Re ζ′ + 3α) + i·sin(9·Im ζ′ + 2α)) (lưới lệch); n₁ = value_noise(Re ζ₀, Im ζ₀; SNF, 3σ + 40), n₂ = value_noise(Re ζ₀, Im ζ₀; SNF, 3σ + 41) (mục 2; ≈ một ô nhiễu mỗi hạt); ζ = ζ₀ + SJIT·(cos 2πn₁ + i·sin 2πn₂) (hạt lệch khỏi nút lưới); θ_h = 0,45 + SSIZ·(2n₁ − 1) (ngưỡng hốc: lớn = hốc nhỏ); dep = 1 + SDEP·(2n₂ − 1) (độ sâu hốc); T = T(ζ; a); P = S((θ_h − T)/0,25); ε = 0,02; P_x = S((θ_h − T(ζ + ε; a))/0,25), P_y = S((θ_h − T(ζ + iε; a))/0,25); g = ((P_x − P) + i(P_y − P))·(amt·dep/ε)·e^{i(α − φ)}; n_x0 = Re n_w, n_y0 = Im n_w, n_z0 = √max(1 − n_x0² − n_y0², 0); k = 0,02·n_z0; u = Re q, v = Im q; g_x = 0,07·cos(6u + 2v + φ) + 0,05·cos(9v − 3u + 2φ), g_y = 0,07·sin(5v − 2,5u + φ) + 0,05·sin(8u + 4v + 3φ) (vỏ gồ nhẹ); n = unit3(n_x0 + k·Re g + g_x·n_z0, n_y0 + k·Im g + g_y·n_z0, n_z0); trả về n, n_z0, T, P·dep, ζ, θ_h.
- **[F-26] `pr_berry_v`** — Quả i kiểu ảnh chụp (v1.1): (sd, q, n_w) = GEO(z, i) (= berry_v); (n, n_z0, T, P, ζ, θ_h) = bumped_v(q, n_w, φ_i, α_i, A_SEED, BUMP·detail, sid_i); P ← P·detail; τ̂ = e^{i(φ_i − π/2)}; seed = S((0,86 + 0,5·(θ_h − 0,45) − T(ζ − 0,025τ̂; A_SEED))/0,06)·(0,25 + 0,75·detail) (hạt vàng to nhỏ theo cùng ngưỡng với hốc); mot = 0,9 + 0,2·(0,5 + 0,5·cos(5u + 3v + 1,3φ_i)·cos(4v − 2u + φ_i)), u = Re q, v = Im q (loang màu); alb_v = ALB_v·mot; so = 0,5 + 0,5·cos(7·Re ζ + 5·Im ζ + sid_i); body = shade_flesh(n, n_z0, P, alb); n·L₀ = max(Re n_w·L_x + Im n_w·L_y + n_z0·L_z, 0); sa_v = ALB_SEED_v·(1 − 0,45·so) + 0,6·ALB_v·so (hạt vàng ↔ cam); sk_v = sa_v·(KEY_v·(0,25 + 0,75·n·L₀) + AMBI)·(0,45 + 0,55·n_z0); (sp, box) = spec(n, box_e); K_v = body_v·(1 − seed) + sk_v·seed + sp. Trả về sd, R_i, K, q, n.
- **[F-27] `berry_dof`** — Quả i (O, v1.1): pr_berry_v(z, i, edge, box_e = BOXE + 0,3·GB_i, detail = 1 − DOFD·GB_i).
- **[F-28] `scene`** — Cảnh (O, macro): H = fold_over(pr_ground(z), pr_layers(z, EDGE, berry_dof, edge_fn)), edge_fn(0, i) = DOFB·GB_i, edge_fn(1, k) = DOFB·GD_k; (H₀, H₁, H₂)_v = encode(H·vignette(x, y; VIG))_v + grain(x, y; GRAIN_A, 520, 99).

### 4.3 Bảng hằng số (P-xx)

| ID | Tên | Giá trị | Ý nghĩa và cơ sở |
|---|---|---|---|
| P-01 | `Q` | `bảng trong code (mục 5)` | bảng neo quả (x, y, r, sid) — x, y, r ĐO (watershed theo khe tối); sid = mã cố định của quả (seed gắn với object); xếp quả sau → quả trước (ƯỚC LƯỢNG: quả to ở trước) |
| P-02 | `DL` | `bảng trong code (mục 5)` | bảng neo đài lá (x, y, s, sid) — x, y, s ĐO (mảng xanh liên thông), s = bán kính tương đương; sid = mã cố định của đài lá |
| P-03 | `LIGHT` | `unit_light(-0.5, 0.6, 1.2)` | hướng sáng: góc 130° ĐO, độ cao ƯỚC LƯỢNG |
| P-04 | `K_S` | `(0.431, 0.061, 0.074)` | đỏ tối, giữa, sáng — ĐO |
| P-05 | `K_M` | `(0.686, 0.133, 0.106)` | đỏ tối, giữa, sáng — ĐO |
| P-06 | `K_L` | `(0.875, 0.133, 0.071)` | đỏ tối, giữa, sáng — ĐO |
| P-07 | `K_GAP` | `(0.184, 0.055, 0.035)` | khe tối, lấp lánh — ĐO |
| P-08 | `K_HL` | `(0.925, 0.827, 0.741)` | khe tối, lấp lánh — ĐO |
| P-09 | `K_G1` | `(0.612, 0.678, 0.31)` | đài lá sáng, tối, hạt — ĐO |
| P-10 | `K_G0` | `(0.427, 0.376, 0.149)` | đài lá sáng, tối, hạt — ĐO |
| P-11 | `K_SEED` | `(0.788, 0.647, 0.325)` | đài lá sáng, tối, hạt — ĐO |
| P-12 | `RS` | `1.1` | RS: bán kính dáng / bán kính đo (bù phần quả bị che) — ƯỚC LƯỢNG |
| P-13 | `KEY` | `(1.0, 1.0, 1.0)` | màu–cường độ đèn chính, môi trường, phơi sáng, điểm gập vai sáng — CHỌN |
| P-14 | `AMBI` | `0.1` | màu–cường độ đèn chính, môi trường, phơi sáng, điểm gập vai sáng — CHỌN |
| P-15 | `EXPO` | `1.0` | màu–cường độ đèn chính, môi trường, phơi sáng, điểm gập vai sáng — CHỌN |
| P-16 | `KNEE` | `0.75` | màu–cường độ đèn chính, môi trường, phơi sáng, điểm gập vai sáng — CHỌN |
| P-17 | `FILLC` | `(0.0, 0.0, 0.0)` | đèn đỡ: màu–cường độ, hướng — CHỌN |
| P-18 | `FILLD` | `(0.8, 0.1, 0.6)` | đèn đỡ: màu–cường độ, hướng — CHỌN |
| P-19 | `BOXW` | `0.3` | softbox: nửa rộng, nửa cao (đơn vị vectơ phản xạ), độ mềm mép, độ chói — CHỌN |
| P-20 | `BOXH` | `0.2` | softbox: nửa rộng, nửa cao (đơn vị vectơ phản xạ), độ mềm mép, độ chói — CHỌN |
| P-21 | `BOXE` | `0.06` | softbox: nửa rộng, nửa cao (đơn vị vectơ phản xạ), độ mềm mép, độ chói — CHỌN |
| P-22 | `BOXI` | `18.0` | softbox: nửa rộng, nửa cao (đơn vị vectơ phản xạ), độ mềm mép, độ chói — CHỌN |
| P-23 | `F0` | `0.03` | Fresnel ở góc thẳng (vỏ ướt), độ chói môi trường — CHỌN |
| P-24 | `ENV` | `2.5` | Fresnel ở góc thẳng (vỏ ướt), độ chói môi trường — CHỌN |
| P-25 | `WRAP` | `(0.45, 0.12, 0.12)` | bọc khuếch tán theo kênh: đỏ thấu sang vùng tối (tán xạ dưới bề mặt) — CHỌN |
| P-26 | `BUMP` | `2.2` | độ nghiêng pháp tuyến ở lỗ hạt, độ tối hốc, mật độ hạt (≈ 14 hạt mỗi đường kính), độ lệch lưới — CHỌN |
| P-27 | `PITD` | `0.5` | độ nghiêng pháp tuyến ở lỗ hạt, độ tối hốc, mật độ hạt (≈ 14 hạt mỗi đường kính), độ lệch lưới — CHỌN |
| P-28 | `A_SEED` | `30.0` | độ nghiêng pháp tuyến ở lỗ hạt, độ tối hốc, mật độ hạt (≈ 14 hạt mỗi đường kính), độ lệch lưới — CHỌN |
| P-29 | `WARP` | `0.03` | độ nghiêng pháp tuyến ở lỗ hạt, độ tối hốc, mật độ hạt (≈ 14 hạt mỗi đường kính), độ lệch lưới — CHỌN |
| P-30 | `BOX2D` | `(0.6, 0.5, 0.62)` | softbox phụ (phải-trên): hướng, nửa rộng, nửa cao, độ chói — CHỌN |
| P-31 | `BOX2W` | `0.25` | softbox phụ (phải-trên): hướng, nửa rộng, nửa cao, độ chói — CHỌN |
| P-32 | `BOX2H` | `0.35` | softbox phụ (phải-trên): hướng, nửa rộng, nửa cao, độ chói — CHỌN |
| P-33 | `BOX2I` | `5.0` | softbox phụ (phải-trên): hướng, nửa rộng, nửa cao, độ chói — CHỌN |
| P-34 | `SHD` | `0.05` | độ dời bóng đổ (theo hướng sáng), độ đậm bóng đổ, độ đậm và bề rộng bóng tiếp xúc (× R) — CHỌN |
| P-35 | `SHA` | `0.55` | độ dời bóng đổ (theo hướng sáng), độ đậm bóng đổ, độ đậm và bề rộng bóng tiếp xúc (× R) — CHỌN |
| P-36 | `CONTA` | `0.7` | độ dời bóng đổ (theo hướng sáng), độ đậm bóng đổ, độ đậm và bề rộng bóng tiếp xúc (× R) — CHỌN |
| P-37 | `CONTW` | `0.25` | độ dời bóng đổ (theo hướng sáng), độ đậm bóng đổ, độ đậm và bề rộng bóng tiếp xúc (× R) — CHỌN |
| P-38 | `FOCS` | `20` | sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN |
| P-39 | `DOFB` | `0.03` | sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN |
| P-40 | `DOFD` | `0.85` | sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN |
| P-41 | `GRAIN_A` | `0.018` | sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN |
| P-42 | `VIG` | `0.22` | sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN |
| P-43 | `SHARP` | `0.35` | sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN |
| P-44 | `SHP` | `0.045` | biên độ méo dáng riêng của từng quả (× bán kính) — CHỌN |
| P-45 | `SJIT` | `0.02` | lệch vị trí hạt, biên độ đổi cỡ hốc, biên độ đổi độ sâu hốc, tần số nhiễu trên mặt quả (≈ 1 ô nhiễu mỗi hạt) — CHỌN |
| P-46 | `SSIZ` | `0.08` | lệch vị trí hạt, biên độ đổi cỡ hốc, biên độ đổi độ sâu hốc, tần số nhiễu trên mặt quả (≈ 1 ô nhiễu mỗi hạt) — CHỌN |
| P-47 | `SDEP` | `0.3` | lệch vị trí hạt, biên độ đổi cỡ hốc, biên độ đổi độ sâu hốc, tần số nhiễu trên mặt quả (≈ 1 ô nhiễu mỗi hạt) — CHỌN |
| P-48 | `SNF` | `4.5` | lệch vị trí hạt, biên độ đổi cỡ hốc, biên độ đổi độ sâu hốc, tần số nhiễu trên mặt quả (≈ 1 ô nhiễu mỗi hạt) — CHỌN |

Các hằng số hình học nằm ngay trong công thức ở 4.2 (0,36; 0,15; 0,85; 0,57…) là một phần định nghĩa dáng, cơ sở CHỌN.

### 4.4 Thứ tự lớp

Lớp: L01, L02, L03, L04, L05, L06; object template: O01, O02 (O01 = quả dâu `berry_v`, tức dáng chung `berry` dãn theo dáng riêng của từng quả; O02 = đài lá). L01 là nền Γ; sau đó, theo thứ tự SEQ (q = quả theo chỉ số dòng Q, d = đài lá theo chỉ số dòng DL):

q0, d4, q1, d10, q2, d6, d9, q3, d8, q4, q5, q6, q7, d7, q8, q9, q10, q11, q12, q13, d3, q14, q15, d0, q16, d5, q17, d1, d11, d13, q18, d2, q19, q20, d12

Mỗi mục quả sinh các lớp L02–L03, mỗi mục đài lá sinh các lớp còn lại như ghi ở `scene` (4.2). Lớp sau đè lớp trước.

## 5. Mã tham chiếu

```python
# === EP SPEC CODE: dong-dau-tay-macro v1.1 ===
# ---------- EP-KERNEL v1.1 (copy nguyên văn vào mọi spec; chỉ numpy + thư viện chuẩn) ----------
import numpy as np, zlib, struct, hashlib

# --- Lưới mẫu & render ---
def sample_grid(W, H, ss=1, i=0, j=0):
    """Lưới tâm mẫu (i,j) trong ss×ss mẫu mỗi pixel: x∈[-A,A], y∈[-1,1] (y hướng lên), A=W/H.
    ss=1, i=j=0 là tâm pixel. Trả về x, y, A, px với px = khoảng cách hai mẫu kề nhau = 2/(H·ss)."""
    A = W / H
    X = ((np.arange(W) + (i + 0.5) / ss) / W * 2.0 - 1.0) * A
    Y = 1.0 - (np.arange(H) + (j + 0.5) / ss) / H * 2.0
    x, y = np.meshgrid(X, Y)                       # shape (H, W)
    return x, y, A, 2.0 / H / ss

def render(scene_fn, W, H, ss=1):
    """Gọi scene_fn(x, y, A, px) cho từng mẫu theo thứ tự j (hàng) ngoài, i (cột) trong; cộng dồn theo đúng
    thứ tự đó rồi chia ss². Trả về ảnh float (H,W,3) CHƯA clip. ss=1 là render tại tâm pixel."""
    acc = None
    for j in range(ss):
        for i in range(ss):
            x, y, A, px = sample_grid(W, H, ss, i, j)
            img = scene_fn(x, y, A, px)
            acc = img if acc is None else acc + img
    return acc / float(ss * ss)

def pix(xn, yn, W, H):
    """Toạ độ chuẩn hoá (xn,yn) → chỉ số pixel (m,n) chứa điểm đó."""
    A = W / H
    m = int(np.floor((xn / A + 1.0) / 2.0 * W)); n = int(np.floor((1.0 - yn) / 2.0 * H))
    return min(max(m, 0), W - 1), min(max(n, 0), H - 1)

# --- Hàm vô hướng ---
def clamp01(t): return np.clip(t, 0.0, 1.0)
def smoothstep(e0, e1, t):
    """Chỉ dùng với e0 < e1 (như GLSL). s = clamp((t−e0)/(e1−e0)); s²(3−2s)."""
    t = clamp01((t - e0) / (e1 - e0)); return t * t * (3.0 - 2.0 * t)
def mix(a, b, t): return a * (1.0 - t) + b * t
def rotate(x, y, cx, cy, ang):
    """(u,v): toạ độ cục bộ trong hệ gốc (cx,cy) quay góc ang (radian, dương = ngược chiều kim đồng hồ)."""
    c, s = np.cos(ang), np.sin(ang); dx, dy = x - cx, y - cy
    return c * dx + s * dy, -s * dx + c * dy
def gauss(x, y, cx, cy, sx, sy, ang=0.0):
    """exp(−(u/sx)² − (v/sy)²): sx, sy là tham số độ rộng đúng theo biểu thức, không phải độ lệch chuẩn."""
    u, v = rotate(x, y, cx, cy, ang); return np.exp(-(u / sx) ** 2 - (v / sy) ** 2)

# --- SDF: âm bên trong, dương bên ngoài, đơn vị = toạ độ chuẩn hoá ---
def sd_circle(x, y, cx, cy, r): return np.hypot(x - cx, y - cy) - r
def sd_ellipse(x, y, cx, cy, a, b, ang=0.0):
    """Xấp xỉ SDF của ellipse bán trục a (theo u), b (theo v); đúng dấu, gần đúng khoảng cách ở sát biên."""
    u, v = rotate(x, y, cx, cy, ang); return (np.hypot(u / a, v / b) - 1.0) * min(a, b)
def sd_box(x, y, cx, cy, hx, hy, ang=0.0, r=0.0):
    u, v = rotate(x, y, cx, cy, ang)
    qx, qy = np.abs(u) - (hx - r), np.abs(v) - (hy - r)
    return np.hypot(np.maximum(qx, 0.0), np.maximum(qy, 0.0)) + np.minimum(np.maximum(qx, qy), 0.0) - r
def sd_segment(x, y, ax, ay, bx, by):
    """Khoảng cách tới đoạn AB (A=B → khoảng cách tới A). Trừ nửa bề rộng để thành nét capsule."""
    dx, dy, ex, ey = x - ax, y - ay, bx - ax, by - ay
    h = clamp01((dx * ex + dy * ey) / max(ex * ex + ey * ey, 1e-18))
    return np.hypot(dx - ex * h, dy - ey * h)
def sd_polyline(x, y, pts):
    """Khoảng cách tới đường gấp khúc hở qua pts (≥ 2 điểm) = min khoảng cách tới từng đoạn."""
    P = np.asarray(pts, dtype=np.float64); d = np.full_like(x, np.inf)
    for k in range(len(P) - 1):
        d = np.minimum(d, sd_segment(x, y, P[k, 0], P[k, 1], P[k + 1, 0], P[k + 1, 1]))
    return d
def bezier_pts(p0, p1, p2, p3, n):
    """Tessellate Bézier bậc ba thành n đoạn: n+1 điểm tại t_k = k/n. n là tham số khoá của spec."""
    t = (np.arange(n + 1, dtype=np.float64) / n)[:, None]; P = np.array([p0, p1, p2, p3], dtype=np.float64)
    return (1 - t) ** 3 * P[0] + 3 * (1 - t) ** 2 * t * P[1] + 3 * (1 - t) * t ** 2 * P[2] + t ** 3 * P[3]
def sd_polygon(x, y, pts):
    """SDF chính xác của đa giác đơn (pts: [(x0,y0), ...], khép kín ngầm; thuật toán Inigo Quilez)."""
    P = np.asarray(pts, dtype=np.float64); N = len(P)
    d = (x - P[0, 0]) ** 2 + (y - P[0, 1]) ** 2; s = np.ones_like(x); j = N - 1
    for i in range(N):
        ex, ey = P[j, 0] - P[i, 0], P[j, 1] - P[i, 1]
        wx, wy = x - P[i, 0], y - P[i, 1]
        t = clamp01((wx * ex + wy * ey) / (ex * ex + ey * ey))
        bx, by = wx - ex * t, wy - ey * t
        d = np.minimum(d, bx * bx + by * by)
        c1, c2, c3 = y >= P[i, 1], y < P[j, 1], ex * wy > ey * wx
        s = np.where((c1 & c2 & c3) | (~c1 & ~c2 & ~c3), -s, s); j = i
    return s * np.sqrt(d)
def polar(x, y, cx, cy, ang=0.0):
    u, v = rotate(x, y, cx, cy, ang); return np.hypot(u, v), np.arctan2(v, u)
def sd_radial(x, y, cx, cy, r_fn, ang=0.0):
    """Hình 'sao' r = r_fn(θ): âm bên trong (xấp xỉ SDF)."""
    r, th = polar(x, y, cx, cy, ang); return r - r_fn(th)

# --- Mask & compositing (màu float [0,1]; K là (3,) hoặc trường (H,W,3)) ---
def mask(sd, edge): return 1.0 - smoothstep(-edge, edge, sd)
def ring(sd, width, edge): return mask(np.abs(sd) - width / 2.0, edge)
def col(h): return np.array([int(h[i:i + 2], 16) / 255.0 for i in (1, 3, 5)])
def over(img, K, M): return img * (1.0 - M)[..., None] + np.asarray(K) * M[..., None]
def add(img, K, M): return img + np.asarray(K) * M[..., None]
def multiply(img, K, M): return img * (1.0 - M[..., None] * (1.0 - np.asarray(K)))
def screen(img, K, M): return 1.0 - (1.0 - img) * (1.0 - np.asarray(K) * M[..., None])
def gradient(t, stops):
    """stops=[(t0,K0),(t1,K1),...] với t tăng dần; nội suy tuyến tính từng đoạn, kẹp ở hai đầu."""
    ts = np.array([s[0] for s in stops], dtype=np.float64)
    Ks = np.array([np.asarray(s[1], dtype=np.float64) for s in stops])
    tf = np.asarray(t, dtype=np.float64).ravel()
    out = np.stack([np.interp(tf, ts, Ks[:, c]) for c in range(3)], axis=-1)
    return out.reshape(np.shape(t) + (3,))
# Tuỳ chọn profile COLOR_SPACE = linear: đổi palette bằng srgb_to_linear khi nạp, đổi ngược bằng linear_to_srgb trước to_uint8.
def srgb_to_linear(c):
    c = np.asarray(c, dtype=np.float64); return np.where(c <= 0.04045, c / 12.92, ((c + 0.055) / 1.055) ** 2.4)
def linear_to_srgb(l):
    l = np.maximum(np.asarray(l, dtype=np.float64), 0.0); return np.where(l <= 0.0031308, 12.92 * l, 1.055 * l ** (1 / 2.4) - 0.055)

# --- Noise tất định (số nguyên 32-bit, không phụ thuộc nền tảng) ---
def hash2(i, j):
    """Hash số nguyên 32-bit → [0,1): n = i·374761393 + j·668265263 + 2654435769 (mod 2^32), rồi trộn lowbias32."""
    i = (np.asarray(i, dtype=np.int64) % 4294967296).astype(np.uint32)
    j = (np.asarray(j, dtype=np.int64) % 4294967296).astype(np.uint32)
    n = i * np.uint32(374761393) + j * np.uint32(668265263) + np.uint32(2654435769)
    n ^= n >> np.uint32(16); n = n * np.uint32(0x7FEB352D)
    n ^= n >> np.uint32(15); n = n * np.uint32(0x846CA68B)
    n ^= n >> np.uint32(16)
    return n.astype(np.float64) / 4294967296.0
def value_noise(x, y, freq, seed=0):
    """Lưới i=⌊x·f⌋+7919·seed, j=⌊y·f⌋ (floor về −∞); nội suy song tuyến tính với trọng số t²(3−2t)."""
    px_, py_ = x * freq, y * freq
    i0, j0 = np.floor(px_), np.floor(py_); fx, fy = px_ - i0, py_ - j0
    i0 = i0.astype(np.int64) + 7919 * int(seed); j0 = j0.astype(np.int64)
    ux, uy = fx * fx * (3.0 - 2.0 * fx), fy * fy * (3.0 - 2.0 * fy)
    v00, v10, v01, v11 = hash2(i0, j0), hash2(i0 + 1, j0), hash2(i0, j0 + 1), hash2(i0 + 1, j0 + 1)
    return mix(mix(v00, v10, ux), mix(v01, v11, ux), uy)
def fbm(x, y, freq, octaves=4, gain=0.5, lacunarity=2.0, seed=0):
    v, amp, norm, f = np.zeros_like(x), 1.0, 0.0, freq
    for o in range(octaves):
        v = v + amp * value_noise(x, y, f, seed + o); norm += amp; amp *= gain; f *= lacunarity
    return v / norm

# --- Xuất ảnh & kiểm chứng ---
def to_uint8(img):
    """Lượng tử hoá: ⌊255·clamp(c,0,1) + 0,5⌋ — làm tròn nửa lên, giống nhau ở mọi ngôn ngữ."""
    return np.floor(np.clip(img, 0.0, 1.0) * 255.0 + 0.5).astype(np.uint8)
def save_png(path, u8):
    """Ghi PNG 8-bit RGB bằng thư viện chuẩn (không cần Pillow)."""
    H, W, _ = u8.shape
    raw = b''.join(b'\x00' + u8[r].tobytes() for r in range(H))
    def chunk(tag, data):
        return struct.pack('>I', len(data)) + tag + data + struct.pack('>I', zlib.crc32(tag + data) & 0xffffffff)
    png = (b'\x89PNG\r\n\x1a\n' + chunk(b'IHDR', struct.pack('>IIBBBBB', W, H, 8, 2, 0, 0, 0))
           + chunk(b'IDAT', zlib.compress(raw, 9)) + chunk(b'IEND', b''))
    with open(path, 'wb') as f: f.write(png)
def pixel_sha256(u8):
    """Hash pixel EP-PIX v1: SHA-256 của b'EP-PIX v1 W H RGB\\n' + bytes RGB uint8 theo hàng từ trên xuống."""
    H, W, _ = u8.shape
    return hashlib.sha256(b"EP-PIX v1 %d %d RGB\n" % (W, H) + np.ascontiguousarray(u8).tobytes()).hexdigest()
def check_probes(u8, expected, tol=2):
    """expected=[(m,n,R,G,B), ...]; in PASS/FAIL từng điểm, trả về True nếu tất cả đạt."""
    ok = True
    for (m, n, R, G, B) in expected:
        r, g, b = (int(v) for v in u8[n, m]); good = max(abs(r - R), abs(g - G), abs(b - B)) <= tol
        ok &= good; print(f"probe ({m},{n}) expected ({R},{G},{B}) got ({r},{g},{b}) -> {'PASS' if good else 'FAIL'}")
    return ok
def check_hash(u8, expected_hex):
    h = pixel_sha256(u8); ok = (h == expected_hex)
    print(f"PIXEL_SHA256 {h} -> {'PIXEL HASH PASS' if ok else 'PIXEL HASH FAIL (expected ' + expected_hex + ')'}")
    return ok
# ---------- hết EP-KERNEL v1.1 ----------

# ---------- OF-KIT v1.1 (Một Công Thức) — bộ công cụ EP-II, dùng kèm EP-KERNEL v1.1; chỉ numpy + thư viện chuẩn ----------
import math, cmath, types, re

def _scalar_backend():
    """Backend vô hướng (math/cmath) để kiểm tra công thức tại từng pixel độc lập với numpy."""
    def _c(fr, fc): return lambda t: fc(t) if isinstance(t, complex) else fr(t)
    def _sqrt(t):
        if isinstance(t, complex): return cmath.sqrt(t)
        return math.sqrt(t) if t >= 0 else float('nan')
    S = types.SimpleNamespace()
    S.exp, S.sin, S.cos, S.sqrt = _c(math.exp, cmath.exp), _c(math.sin, cmath.sin), _c(math.cos, cmath.cos), _sqrt
    S.arcsin, S.arctan2, S.hypot, S.floor, S.abs, S.pi = math.asin, math.atan2, math.hypot, math.floor, abs, math.pi
    S.maximum, S.minimum = (lambda a, b: a if a >= b else b), (lambda a, b: a if a <= b else b)
    S.clip = lambda t, a, b: a if t < a else (b if t > b else t)
    S.real, S.imag, S.angle, S.conj = (lambda z: z.real), (lambda z: z.imag), cmath.phase, (lambda z: z.conjugate())
    return S
SCALAR = _scalar_backend()
M = np                       # backend đang dùng: np khi render; SCALAR khi check_pointwise. Công thức chỉ gọi M.*

# --- Cổng và bước ---
def gate(u):
    """Cổng Yeganeh Ĝ(u) = exp(−exp(min(u, 50))): ≈1 khi u ≪ 0, ≈0 khi u ≫ 0; kẹp u để không tràn số."""
    return M.exp(-M.exp(M.minimum(u, 50.0)))
def sstep(d):
    """Bước mềm EP dạng đóng: S(δ) = ¼(1−δ̂)²(2+δ̂), δ̂ = clip(δ, −1, 1); bằng 1 − smoothstep(−1, 1, δ). Dùng δ = sd/EDGE."""
    d = M.clip(d, -1.0, 1.0); return 0.25 * (1.0 - d) ** 2 * (2.0 + d)

# --- Gộp lớp dạng đóng ---
def fold_over(bg, layers):
    """H_v = Γ_v·Π(1−M_k) + Σ_k M_k·K_{k,v}·Π_{j>k}(1−M_j). bg và mỗi K là bộ 3 (vô hướng hoặc trường); lớp sau đè lớp trước."""
    H = list(bg)
    for Mk, Kk in layers:
        for v in range(3): H[v] = H[v] * (1.0 - Mk) + Kk[v] * Mk
    return tuple(H)

# --- Toạ độ phức, đặt vật, khối cầu, lưới ---
def spiral(s, rho, offset=0.0):
    """Xoắn ốc góc vàng: c_s = ρ·√(s − ½)·e^{iγs} + offset, γ = π(3 − √5)."""
    return rho * M.sqrt(s - 0.5) * M.exp(1j * M.pi * (3.0 - M.sqrt(5.0)) * s) + offset
def unit_light(lx, ly, lz):
    n = math.sqrt(lx * lx + ly * ly + lz * lz); return (lx / n, ly / n, lz / n)
def sphere(w, light, shin=60.0):
    """w = (z − c)/R. Trả về τ = min(|w|, 1), khuếch tán d = max(n·L, 0), bóng p = max(n·H, 0)^shin; n = (Re w, Im w, √(1−τ²))."""
    tau = M.minimum(M.abs(w), 1.0); nz = M.sqrt(1.0 - tau * tau); nx, ny = M.real(w), M.imag(w)
    lx, ly, lz = light
    d = M.maximum(nx * lx + ny * ly + nz * lz, 0.0)
    hx, hy, hz = lx, ly, lz + 1.0; hn = math.sqrt(hx * hx + hy * hy + hz * hz)
    p = M.maximum((nx * hx + ny * hy + nz * hz) / hn, 0.0) ** shin
    return tau, d, p
def sphere_map(w):
    """ζ = arcsin(τ)·e^{iφ}: toạ độ trên mặt cầu; lưới vẽ theo ζ tự dày lên ở mép."""
    return M.arcsin(M.minimum(M.abs(w), 1.0)) * M.exp(1j * M.angle(w))
def lattice(zeta, a, b=1.25):
    """T = cos(a·Re ζ)·cos(b·a·Im ζ) ∈ [−1, 1]."""
    return M.cos(a * M.real(zeta)) * M.cos(b * a * M.imag(zeta))
def quad3(v, c0, c1, c2):
    """Đa thức bậc hai theo kênh v = 0, 1, 2 đi qua (c0, c1, c2) — dạng viết gọn một màu trong công thức."""
    return c0 * (v - 1) * (v - 2) / 2.0 - c1 * v * (v - 2) + c2 * v * (v - 1) / 2.0

def _h2(i, j):
    """hash2 của kernel khi render bằng numpy; bản số nguyên thuần (cùng bit) khi kiểm tra vô hướng."""
    if M is np: return hash2(i, j)
    n = ((int(i) % 4294967296) * 374761393 + (int(j) % 4294967296) * 668265263 + 2654435769) & 0xFFFFFFFF
    n ^= n >> 16; n = (n * 0x7FEB352D) & 0xFFFFFFFF; n ^= n >> 15; n = (n * 0x846CA68B) & 0xFFFFFFFF; n ^= n >> 16
    return n / 4294967296.0
def worley(x, y, freq, seed=0):
    """Worley/Voronoi F1: khoảng cách (đơn vị ô) tới hạt gần nhất; mỗi ô lưới tần số freq có một hạt đặt bằng hash; tất định."""
    px_, py_ = x * freq, y * freq
    i0, j0 = M.floor(px_), M.floor(py_); best = None
    for dj in (-1, 0, 1):
        for di in (-1, 0, 1):
            ci, cj = i0 + di, j0 + dj
            d = M.hypot(ci + _h2(ci + 7919 * seed, cj) - px_, cj + _h2(cj + 7919 * seed, ci + 1) - py_)
            best = d if best is None else M.minimum(best, d)
    return best

# --- Render EP-II: scene trả về bộ 3 kênh (H0, H1, H2) ---
def render_of(scene_fn, W, H, ss=1):
    """Như render() của kernel nhưng scene trả về (H0, H1, H2); trả về ảnh float (H,W,3) chưa clip."""
    acc = None
    with np.errstate(over='ignore'):                 # hash số nguyên 32-bit cố ý tràn (wrap); tắt cảnh báo khi gọi noise tại điểm vô hướng
        for j in range(ss):
            for i in range(ss):
                x, y, A, px = sample_grid(W, H, ss, i, j)
                H0, H1, H2 = scene_fn(x, y, A, px)
                img = np.stack([np.broadcast_to(np.asarray(c, dtype=np.float64), x.shape) for c in (H0, H1, H2)], axis=-1)
                acc = img if acc is None else acc + img
    return acc / float(ss * ss)

def check_pointwise(scene_fn, u8, W, H, ss=1, n=100, tol=1, seed=1):
    """Test A của Một Công Thức: tính lại n pixel chọn bằng hash2 bằng backend vô hướng (math/cmath), so với render."""
    g = scene_fn.__globals__; old = g['M']; g['M'] = SCALAR; bad = 0
    try:
        with np.errstate(over='ignore'):
            for k in range(n):
                m = int(hash2(np.array([k]), np.array([seed]))[0] * W); nn = int(hash2(np.array([seed]), np.array([k]))[0] * H)
                m, nn = min(m, W - 1), min(nn, H - 1); A = W / H; acc = [0.0, 0.0, 0.0]
                for j in range(ss):
                    for i in range(ss):
                        xs = ((m + (i + 0.5) / ss) / W * 2.0 - 1.0) * A; ys = 1.0 - (nn + (j + 0.5) / ss) / H * 2.0
                        c = scene_fn(xs, ys, A, 2.0 / H / ss)
                        for v in range(3): acc[v] += float(np.real(c[v]))
                rgb = [math.floor(min(max(a / (ss * ss), 0.0), 1.0) * 255.0 + 0.5) for a in acc]
                if max(abs(int(u8[nn, m, v]) - rgb[v]) for v in range(3)) > tol: bad += 1
    finally:
        g['M'] = old
    print(f"POINTWISE {n - bad}/{n} pixel khớp (±{tol}) -> {'POINTWISE PASS' if bad == 0 else 'POINTWISE FAIL'}")
    return bad == 0

# --- Đo công thức và so khác biệt ---
def measure_formula(code_text, start="# ===== CÔNG THỨC =====", end="# ===== HẾT CÔNG THỨC ====="):
    """Đếm ký tự (bỏ chú thích, dòng trống, khoảng trắng) và hằng số (mọi literal số) của phần giữa hai dòng mốc."""
    m = re.search(r"^" + re.escape(start) + r"[ \t]*\n(.*?)^" + re.escape(end), code_text, flags=re.S | re.M)
    body = re.sub(r"#[^\n]*", "", m.group(1))
    body = "\n".join(l for l in body.splitlines() if l.strip())
    chars = len(re.sub(r"\s+", "", body))
    consts = len(re.findall(r"(?<![\w.])(?:\d+\.\d*|\.\d+|\d+)(?:e[+-]?\d+)?j?", body))
    return chars, consts, body.count("\n") + 1
def dhash(u8, size=8):
    """dHash 64 bit trên độ sáng: nén về (size+1)×size bằng trung bình khối, bit = sáng hơn pixel bên trái."""
    L = 0.299 * u8[..., 0] + 0.587 * u8[..., 1] + 0.114 * u8[..., 2]
    rows = np.array_split(np.arange(L.shape[0]), size); cols = np.array_split(np.arange(L.shape[1]), size + 1)
    S = np.array([[L[np.ix_(r, c)].mean() for c in cols] for r in rows])
    bits = (S[:, 1:] > S[:, :-1]).ravel()
    return int("".join("1" if b else "0" for b in bits), 2)
def hamming(a, b): return bin(a ^ b).count("1")
def proxies(u8):
    """Chỉ số phụ trợ (không cộng thành điểm thẩm mỹ): clip%, dải sáng p5–p95, bão hoà TB, entropy sắc độ, mật độ biên, cân bằng góc phần tư, lệch tiêu điểm."""
    f = u8.astype(np.float64) / 255.0; mx, mn = f.max(axis=2), f.min(axis=2)
    L = 0.299 * f[..., 0] + 0.587 * f[..., 1] + 0.114 * f[..., 2]
    clip = float(((u8 == 0) | (u8 == 255)).any(axis=2).mean() * 100)
    p5, p95 = np.percentile(L, [5, 95]); sat = float(np.where(mx > 0, (mx - mn) / np.maximum(mx, 1e-9), 0).mean())
    hue = np.arctan2(np.sqrt(3) * (f[..., 1] - f[..., 2]), 2 * f[..., 0] - f[..., 1] - f[..., 2]); hsel = hue[(mx - mn) > 0.15]
    if hsel.size: h, _ = np.histogram(hsel, bins=12, range=(-np.pi, np.pi)); p = h / h.sum(); p = p[p > 0]; hent = float(-(p * np.log2(p)).sum())
    else: hent = 0.0
    gx, gy = np.abs(np.diff(L, axis=1))[:-1, :], np.abs(np.diff(L, axis=0))[:, :-1]; E = gx + gy
    h2, w2 = E.shape[0] // 2, E.shape[1] // 2
    q = np.array([E[:h2, :w2].mean(), E[:h2, w2:].mean(), E[h2:, :w2].mean(), E[h2:, w2:].mean()])
    Hh, Ww = L.shape; ys, xs = np.mgrid[0:Hh - 1, 0:Ww - 1]; wsum = E.sum() + 1e-9
    cx, cy = (E * xs).sum() / wsum / (Ww - 1), (E * ys).sum() / wsum / (Hh - 1)
    thirds = [(a, b) for a in (1 / 3, 2 / 3) for b in (1 / 3, 2 / 3)]; foc = min(math.hypot(cx - a, cy - b) for a, b in thirds)
    return dict(clip_pct=round(clip, 2), lum_p5=round(float(p5), 3), lum_p95=round(float(p95), 3), sat=round(sat, 3), hue_entropy=round(hent, 2),
                edge=round(float(E.mean()), 4), quad_balance=round(float(q.std() / (q.mean() + 1e-9)), 2), focal_offset=round(foc, 3))
# ---------- hết OF-KIT v1.1 ----------

# ===== CÔNG THỨC =====
W, H, SS = 1108, 1108, 2                                   # khung chuẩn 2 × nguồn (A = 1), mẫu mỗi cạnh pixel
# P-01 bảng neo quả (x, y, r, sid) — x, y, r ĐO (watershed theo khe tối); sid = mã cố định của quả (seed gắn với object); xếp quả sau → quả trước (ƯỚC LƯỢNG: quả to ở trước)
Q = ((-0.92, -0.01, 0.1, 0), (-0.01, -0.89, 0.131, 1), (0.92, 0.7, 0.135, 2), (0.01, -0.37, 0.144, 3), (0.03, 0.92, 0.145, 4), (-0.63, -0.88, 0.158, 5),
     (0.78, -0.78, 0.176, 6), (-0.89, 0.77, 0.183, 7), (0.89, -0.19, 0.185, 8), (-0.42, 0.89, 0.187, 9), (0.54, 0.89, 0.214, 10), (0.57, 0.62, 0.219, 11),
     (0.36, -0.82, 0.227, 12), (-0.84, -0.5, 0.245, 13), (0.77, 0.28, 0.251, 14), (0.51, -0.22, 0.259, 15), (-0.28, -0.7, 0.263, 16), (-0.01, 0.61, 0.279, 17),
     (-0.54, -0.09, 0.289, 18), (-0.64, 0.47, 0.322, 19), (-0.01, 0.14, 0.337, 20))
# P-02 bảng neo đài lá (x, y, s, sid) — x, y, s ĐO (mảng xanh liên thông), s = bán kính tương đương; sid = mã cố định của đài lá
DL = ((0.41, -0.46, 0.12, 0), (0.31, 0.62, 0.109, 1), (-0.38, -0.35, 0.095, 2), (-0.87, -0.8, 0.075, 3), (-0.93, -0.12, 0.069, 4), (-0.12, -0.88, 0.069, 5),
      (0.82, 0.6, 0.058, 6), (-0.75, 0.92, 0.05, 7), (0.04, -0.48, 0.039, 8), (0.95, 0.86, 0.034, 9), (0.1, -0.98, 0.032, 10), (0.23, 0.8, 0.03, 11),
      (-0.19, -0.13, 0.028, 12), (-0.27, 0.49, 0.025, 13))
LIGHT = unit_light(-0.5, 0.6, 1.2)                         # P-03 hướng sáng: góc 130° ĐO, độ cao ƯỚC LƯỢNG
HV = unit_light(LIGHT[0], LIGHT[1], LIGHT[2] + 1.0)        # vectơ nửa đường (Blinn), mắt nhìn theo +z
LXY = complex(LIGHT[0], LIGHT[1]) / math.hypot(LIGHT[0], LIGHT[1])
K_S, K_M, K_L = (0.431, 0.061, 0.074), (0.686, 0.133, 0.106), (0.875, 0.133, 0.071)   # P-04..06 đỏ tối, giữa, sáng — ĐO
K_GAP, K_HL = (0.184, 0.055, 0.035), (0.925, 0.827, 0.741)                            # P-07..08 khe tối, lấp lánh — ĐO
K_G1, K_G0, K_SEED = (0.612, 0.678, 0.31), (0.427, 0.376, 0.149), (0.788, 0.647, 0.325)  # P-09..11 đài lá sáng, tối, hạt — ĐO
NQ, ND, RS = len(Q), len(DL), 1.1                         # P-12 RS: bán kính dáng / bán kính đo (bù phần quả bị che) — ƯỚC LƯỢNG
def _qc(i): return complex(Q[i][0], Q[i][1])   # [F-01]
def _host(k):                                              # quả chủ của đài lá k: quả trước nhất chứa tâm, nếu không có thì quả gần nhất theo d/r   [F-02]
    cz = complex(DL[k][0], DL[k][1]); ins = [i for i in range(NQ) if abs(cz - _qc(i)) < Q[i][2]]
    return max(ins) if ins else min(range(NQ), key=lambda i: abs(cz - _qc(i)) / Q[i][2])
HOST = [_host(k) for k in range(ND)]
def _pose(i):                                              # (tâm, bán kính dáng, góc khung α: +v về cuống, độ thuôn ε, pha hạt)   [F-03]
    ks = [k for k in range(ND) if HOST[k] == i]
    if ks:                                                 # chóp quả hướng ra xa đài lá chủ; đài lá gần tâm → nhìn từ trên, quả tròn
        dv = min((_qc(i) - complex(DL[k][0], DL[k][1]) for k in ks), key=abs)
        beta, ep = cmath.phase(dv), min(max((abs(dv) / Q[i][2] - 0.15) / 0.5, 0.0), 1.0)
    else:                                                  # không thấy đài lá: chóp chúc xuống, lệch theo chỉ số (CHỌN)
        beta, ep = -math.pi / 2 + 0.7 * math.cos(2.3 * Q[i][3] + 1.0), 1.0
    return _qc(i), RS * Q[i][2], beta + math.pi / 2, ep, 1.7 * Q[i][3]   # hướng mặc định và pha hạt theo sid
POSE = [_pose(i) for i in range(NQ)]
SEQ = [it for i in range(NQ) for it in [(0, i)] + [(1, k) for k in range(ND) if HOST[k] == i]]   # thứ tự lớp: quả rồi đài lá của nó
E3 = complex(math.cos(2 * math.pi / 3), math.sin(2 * math.pi / 3))

def berry(z, i):
    """Dáng dâu chung: toạ độ cục bộ q (đĩa đơn vị nắn thuôn về chóp, vai hơi lõm ở cuống), SDF xấp xỉ, pháp tuyến trong hệ ảnh."""   # [F-04]
    c, R, al, ep, ph = POSE[i]
    om = (z - c) * complex(math.cos(-al), math.sin(-al)) / R
    u, v = M.real(om), M.imag(om)
    vt = M.maximum(v, 0.0)
    q = u / M.maximum(1.0 + 0.36 * ep * v, 0.3) + 1j * (v + 0.15 * ep * vt * vt * M.exp(-6.0 * u * u)) / (1.0 + 0.1 * ep)
    return (M.abs(q) - 1.0) * R * 0.85, q, q * complex(math.cos(al), math.sin(al))
def surf(q, ph):
    """Toạ độ trên mặt quả: ζ = q·(1 + 0,57|q|²) (xấp xỉ arcsin τ/τ, dày lên ở mép), xoay pha hạt ph."""   # [F-05]
    t2 = M.real(q) ** 2 + M.imag(q) ** 2
    return q * (1.0 + 0.57 * M.minimum(t2, 1.0)) * complex(math.cos(ph), math.sin(ph))
def pw(t, n):   # [F-06]
    """tⁿ với n là luỹ thừa của 2 (bình phương lặp) — nhanh hơn pow tổng quát, cùng giá trị ở mọi backend."""
    while n > 1: t, n = t * t, n // 2
    return t
def hexlat(zeta, a):
    """Lưới lục giác trên mặt cầu: (cos aX₁ + cos aX₂ + cos aX₃)/3, Xₖ = Re(ζ·e^{2πik/3}); bằng 1 tại tâm hạt."""   # [F-07]
    return (M.cos(a * M.real(zeta)) + M.cos(a * M.real(zeta * E3)) + M.cos(a * M.real(zeta / E3))) / 3.0
VIEW = None                                                # khung đang tính (x₀, x₁, y₀, y₁); None = toàn ảnh. Chỉ để bỏ qua lớp chắc chắn bằng 0
def near(c, rad):   # [F-08]
    """Lớp tâm c có thể khác 0 trong khung đang tính không. Mặt nạ của lớp bằng 0 tuyệt đối khi |z − c| ≥ rad, nên bỏ qua không đổi ảnh."""
    return VIEW is None or (VIEW[0] < c.real + rad and VIEW[1] > c.real - rad and VIEW[2] < c.imag + rad and VIEW[3] > c.imag - rad)
# ---- Lõi "ảnh chụp" (lô N–S): chiếu sáng tuyến tính kiểu vật lý; mọi màu tính trong không gian tuyến tính, mã hoá sRGB từng mẫu ở cuối ----
def lin(c):   # [F-09]
    """sRGB → tuyến tính (IEC 61966-2-1) cho HẰNG SỐ màu."""
    return tuple(x / 12.92 if x <= 0.04045 else ((x + 0.055) / 1.055) ** 2.4 for x in c)
KEY, AMBI, EXPO, KNEE = (1.0, 1.0, 1.0), 0.1, 1.0, 0.75   # P-13..16 màu–cường độ đèn chính, môi trường, phơi sáng, điểm gập vai sáng — CHỌN
FILLC, FILLD = (0.0, 0.0, 0.0), (0.8, 0.1, 0.6)            # P-17..18 đèn đỡ: màu–cường độ, hướng — CHỌN
BOXW, BOXH, BOXE, BOXI = 0.3, 0.2, 0.06, 18.0              # P-19..22 softbox: nửa rộng, nửa cao (đơn vị vectơ phản xạ), độ mềm mép, độ chói — CHỌN
F0, ENV = 0.03, 2.5                                        # P-23..24 Fresnel ở góc thẳng (vỏ ướt), độ chói môi trường — CHỌN
WRAP = (0.45, 0.12, 0.12)                                  # P-25 bọc khuếch tán theo kênh: đỏ thấu sang vùng tối (tán xạ dưới bề mặt) — CHỌN
BUMP, PITD, A_SEED, WARP = 2.2, 0.5, 30.0, 0.03            # P-26..29 độ nghiêng pháp tuyến ở lỗ hạt, độ tối hốc, mật độ hạt (≈ 14 hạt mỗi đường kính), độ lệch lưới — CHỌN
BOX2D, BOX2W, BOX2H, BOX2I = (0.6, 0.5, 0.62), 0.25, 0.35, 5.0   # P-30..33 softbox phụ (phải-trên): hướng, nửa rộng, nửa cao, độ chói — CHỌN
SHD, SHA, CONTA, CONTW = 0.05, 0.55, 0.7, 0.25             # P-34..37 độ dời bóng đổ (theo hướng sáng), độ đậm bóng đổ, độ đậm và bề rộng bóng tiếp xúc (× R) — CHỌN
ALB = tuple(x / 1.05 * s for x, s in zip(lin(K_L), (1.0, 0.8, 0.8)))   # albedo thịt quả = đỏ sáng ĐO đổi tuyến tính, chia tổng sáng ở vai quả, G và B × 0,8 (đỏ sâu hơn)
ALB_SEED, ALB_G1, ALB_G0, GAPL, SL = lin(K_SEED), lin(K_G1), lin(K_G0), lin(K_GAP), lin(K_S)
_n = math.hypot(LIGHT[0], LIGHT[1]); UB = (-LIGHT[1] / _n, LIGHT[0] / _n, 0.0)        # trục ngang của softbox (⟂ L)
VB = (LIGHT[1] * UB[2] - LIGHT[2] * UB[1], LIGHT[2] * UB[0] - LIGHT[0] * UB[2], LIGHT[0] * UB[1] - LIGHT[1] * UB[0])   # trục dọc = L × UB
_f = math.sqrt(sum(c * c for c in FILLD)); FL = tuple(c / _f for c in FILLD)
_g = math.sqrt(sum(c * c for c in BOX2D)); L2 = tuple(c / _g for c in BOX2D); _n2 = math.hypot(L2[0], L2[1]); UB2 = (-L2[1] / _n2, L2[0] / _n2, 0.0)
VB2 = (L2[1] * UB2[2] - L2[2] * UB2[1], L2[2] * UB2[0] - L2[0] * UB2[2], L2[0] * UB2[1] - L2[1] * UB2[0])
def tone(x):   # [F-10]
    """Vai sáng: giữ nguyên dưới KNEE, trên KNEE cong mềm về 1 (liên tục, trơn bậc 1)."""
    return KNEE + (1.0 - KNEE) * (1.0 - M.exp(-(M.maximum(x, KNEE) - KNEE) / (1.0 - KNEE))) + M.minimum(x, KNEE) - KNEE
def encode(H):   # [F-11]
    """Tuyến tính → (phơi sáng, vai sáng) → sRGB (hàm linear_to_srgb của kernel), từng mẫu."""
    return tuple(linear_to_srgb(tone(EXPO * h)) for h in H)
def unit3(x, y, z_):   # [F-12]
    s = 1.0 / M.sqrt(x * x + y * y + z_ * z_ + 1e-12); return x * s, y * s, z_ * s
def spec(nx, ny, nz, box_e=None):   # [F-13]
    """Phản xạ gương: R = 2(n·V)n − V, V = +z; softbox chữ nhật quanh L (mép mềm box_e), môi trường sáng dần lên trên; nhân Fresnel Schlick."""
    e = BOXE if box_e is None else box_e
    rx, ry, rz = 2.0 * nz * nx, 2.0 * nz * ny, 2.0 * nz * nz - 1.0
    a, b = rx * UB[0] + ry * UB[1] + rz * UB[2], rx * VB[0] + ry * VB[1] + rz * VB[2]
    box = sstep((M.abs(a) - BOXW) / e) * sstep((M.abs(b) - BOXH) / e) * M.clip((rx * LIGHT[0] + ry * LIGHT[1] + rz * LIGHT[2] - 0.3) / 0.3, 0.0, 1.0)
    a2, b2 = rx * UB2[0] + ry * UB2[1] + rz * UB2[2], rx * VB2[0] + ry * VB2[1] + rz * VB2[2]
    box2 = sstep((M.abs(a2) - BOX2W) / e) * sstep((M.abs(b2) - BOX2H) / e) * M.clip((rx * L2[0] + ry * L2[1] + rz * L2[2] - 0.3) / 0.3, 0.0, 1.0)
    env = ENV * 0.06 * (0.25 + 0.75 * M.clip(0.5 + 0.5 * ry, 0.0, 1.0)) + BOX2I * box2
    t = M.clip(1.0 - nz, 0.0, 1.0); fr = F0 + (1.0 - F0) * pw(t, 4) * t
    return fr * (BOXI * box + env), box
def shade_flesh(nx, ny, nz, nz0, P, alb, sss=None):   # [F-14]
    """Thịt quả: khuếch tán bọc theo kênh (tán xạ dưới bề mặt) dưới đèn chính KEY + đèn đỡ FILLC + môi trường; tối ở mép và trong hốc."""
    sss = WRAP if sss is None else sss
    nl = nx * LIGHT[0] + ny * LIGHT[1] + nz * LIGHT[2]; nf = M.maximum(nx * FL[0] + ny * FL[1] + nz * FL[2], 0.0)
    ao = (0.32 + 0.68 * M.sqrt(nz0)) * (1.0 - PITD * P)
    return tuple(alb[v] * (KEY[v] * M.clip((nl + sss[v]) / (1.0 + sss[v]), 0.0, 1.0) + FILLC[v] * nf + AMBI * (0.55 + 0.45 * nz)) * ao for v in range(3))
def sepal(z, k):   # [F-15]
    """Đài lá k (cánh hình mác như calyx2 bản vòng 3) + toạ độ cánh có dấu e (để gập gân giữa)."""
    c, rho, sk = complex(DL[k][0], DL[k][1]), 1.75 * DL[k][2], DL[k][3]; m = 7 + sk % 3                # seed của đài lá = sid
    w = (z - c) / rho; r, psi = M.abs(w), M.angle(w)
    a = (psi + M.pi) * m / (2.0 * M.pi) + 0.37 * sk; j = M.floor(a + 0.5); e = a - j
    jm = j - m * M.floor(j / m); Lk = 0.75 + 0.4 * _h2(jm + 31 * sk, 5); wj = 0.9 + 0.1 * _h2(jm + 13 * sk, 3)   # dài, rộng riêng từng cánh (rộng ≤ 1: không vệt nối)
    prof = M.maximum(1.0 - 2.0 * M.abs(e) / wj, 0.0)
    return (r - (0.18 + (Lk - 0.18) * prof ** 0.6)) * rho * 0.45, r, w, e / wj, Lk                     # cánh hình mác đầy, mũi nhọn, chập ở gốc
def pr_sepal_color(r, w, e, Lk):   # [F-16]
    """Cánh đài: gốc nằm trên quả, ngọn cong lên; gập dọc gân giữa; xanh thấu sáng khi ngược sáng; ngọn hơi khô nâu."""
    t = M.clip(r / Lk, 0.0, 1.0); th = 0.05 + 1.0 * (1.0 - t) ** 1.5; rr = M.maximum(r, 1e-9); cx, cy = M.real(w) / rr, M.imag(w) / rr
    nx, ny, nz = unit3(M.sin(th) * cx - 0.9 * e * cy, M.sin(th) * cy + 0.9 * e * cx, M.cos(th))
    nl = nx * LIGHT[0] + ny * LIGHT[1] + nz * LIGHT[2]
    dry = 0.45 * sstep((0.88 - t) / 0.06); pe = M.maximum(1.0 - 2.0 * M.abs(e), 0.0)
    rim_l = 0.35 * sstep((pe - 0.22) / 0.12); vein = 0.3 * sstep((0.93 - pe) / 0.03) * sstep((t - 0.85) / 0.1)   # mép cánh sáng, gân giữa tối
    alb = tuple(((ALB_G0[v] + (ALB_G1[v] - ALB_G0[v]) * (0.3 + 0.7 * t)) * (1.0 - vein) * (1.0 - rim_l) + ALB_G1[v] * 1.35 * rim_l) * (1.0 - dry) + ALB_G0[v] * 0.55 * dry for v in range(3))
    sp, box = spec(nx, ny, nz, 0.12)
    K = tuple(alb[v] * (KEY[v] * (M.maximum(nl, 0.0) + 0.35 * M.maximum(-nl, 0.0)) + FILLC[v] * 0.5 + AMBI) * (0.6 + 0.4 * t) + 0.5 * sp for v in range(3))
    st = sstep((r - 0.1) / 0.025); sl = 0.55 + 0.45 * M.clip(1.0 + (M.real(w) * LXY.real + M.imag(w) * LXY.imag) / 0.1, 0.0, 2.0) * 0.5   # cuống: đĩa nhìn từ đầu, sáng phía đón sáng
    return tuple(K[v] * (1.0 - st) + ALB_G1[v] * (KEY[v] * sl + AMBI) * 0.8 * st for v in range(3))
def pr_ground(z):   # [F-17]
    """Khe: quả chìm trong tối (vòm Worley) tô tuyến tính."""
    dome = M.clip(1.0 - worley(M.real(z), M.imag(z), 4.5, 3) / 0.8, 0.0, 1.0) ** 2
    return tuple(GAPL[v] * (0.45 + 0.3 * dome) + (SL[v] - GAPL[v]) * 0.18 * dome * dome for v in range(3))
BLACK = (0.0, 0.0, 0.0)
GEO, RADK = berry, 2.6                                      # hình học quả dùng cho lớp (thẻ có thể thay), hệ số bán kính bỏ qua lớp
def pr_layers(z, EDGE, berry_fn, edge_fn=None):   # [F-18]
    """Lớp chung: bóng đổ của quả (dời ngược hướng sáng) → bóng tiếp xúc → quả; bóng đài lá → đài lá. edge_fn(kind, i) cho độ mềm biên riêng."""
    for kind, i in SEQ:
        if kind == 0:
            c, R = POSE[i][0], POSE[i][1]
            if not near(c, RADK * R + SHD): continue
            ed = EDGE if edge_fn is None else EDGE + edge_fn(0, i)
            yield SHA * sstep(GEO(z + SHD * LXY, i)[0] / (0.3 * R)), BLACK                         # L02 bóng đổ của quả i
            sd, R, K = berry_fn(z, i, ed)[:3]
            yield CONTA * M.clip(1.0 - sd / (CONTW * R), 0.0, 1.0) ** 2, BLACK                     # L03 bóng tiếp xúc
            yield sstep(sd / ed), K                                                                 # L04 quả i (O01)
        else:
            if not near(complex(DL[i][0], DL[i][1]), 2.2 * DL[i][2] + 0.09): continue
            yield 0.5 * sstep(sepal(z + 0.03 * LXY, i)[0] / 0.012), BLACK                         # L05 bóng đài lá
            sd, r, w, e, Lk = sepal(z, i); ed = EDGE if edge_fn is None else EDGE + edge_fn(1, i)
            yield sstep(sd / ed), pr_sepal_color(r, w, e, Lk)                                       # L06 đài lá i (O02)
def grain(x, y, amt, f=520.0, seed=99):   # [F-19]
    """Hạt ảnh (đơn sắc, theo toạ độ cảnh): amt·(value_noise − ½); cộng sau khi mã hoá."""
    return amt * (value_noise(x, y, f, seed) - 0.5)
def vignette(x, y, k): return 1.0 - k * (x * x + y * y) / 2.0   # [F-20]
OUT = "dong-dau-tay-macro_render.png"
FOCS, DOFB, DOFD, GRAIN_A, VIG, SHARP = 20, 0.03, 0.85, 0.018, 0.22, 0.35   # P-38..43 sid của quả tiêu điểm, độ mềm biên lớn nhất, độ mất chi tiết lớn nhất, hạt ảnh, tối góc — CHỌN
FOCI = [j for j in range(NQ) if Q[j][3] == FOCS][0]                # dòng của quả tiêu điểm
def _g(c):                                                      # mức mất nét theo khoảng cách tới quả tiêu điểm (0 = nét)   [F-21]
    return min(max(abs(c - POSE[FOCI][0]) - SHARP, 0.0) / 0.9, 1.0) ** 1.3
GB = [_g(POSE[i][0]) * (0.75 + 0.25 * (1.0 - Q[i][2] / 0.337)) for i in range(NQ)]   # quả nhỏ (xa hơn) mờ thêm
GD = [_g(complex(DL[k][0], DL[k][1])) for k in range(ND)]
SHP = 0.045                                                    # P-44 biên độ méo dáng riêng của từng quả (× bán kính) — CHỌN
def _hc(i, j):   # [F-22]
    """hash2 cho hằng số, số nguyên thuần (cùng bit với hash2 của kernel)."""
    n = ((i % 4294967296) * 374761393 + (j % 4294967296) * 668265263 + 2654435769) & 0xFFFFFFFF
    n ^= n >> 16; n = (n * 0x7FEB352D) & 0xFFFFFFFF; n ^= n >> 15; n = (n * 0x846CA68B) & 0xFFFFFFFF; n ^= n >> 16
    return n / 4294967296.0
def _shape(s):                                                 # hệ số dáng của quả có sid s: vai/chóp b₁, méo bậc 2 và 3 (biên độ, pha) — hash theo sid   [F-23]
    h = [_hc(s + 401, k) for k in range(5)]
    return SHP * (1.6 * h[0] - 0.5), SHP * (0.4 + 0.6 * h[1]), 2 * math.pi * h[2], SHP * (0.15 + 0.35 * h[3]), 2 * math.pi * h[4]
SHAPE = [_shape(Q[i][3]) for i in range(NQ)]
def berry_v(z, i):   # [F-24]
    """Dáng riêng của quả i: dáng chung `berry` dãn theo bán kính r(θ) = 1 + b₁ sin θ + a₂ cos(2θ + f₂) + a₃ cos(3θ + f₃), θ = góc trong khung quả (+v về cuống)."""
    c, R, al, ep, ph = POSE[i]; b1, a2, f2, a3, f3 = SHAPE[i]
    th = M.angle((z - c) * complex(math.cos(-al), math.sin(-al)))
    r = 1.0 + b1 * M.sin(th) + a2 * M.cos(2.0 * th + f2) + a3 * M.cos(3.0 * th + f3)
    sd, q, nw = berry(c + (z - c) / r, i)
    return sd * r, q, nw
GEO = berry_v                                                  # các lớp (bóng đổ, bóng tiếp xúc, quả) dùng dáng riêng
SJIT, SSIZ, SDEP, SNF = 0.02, 0.08, 0.3, 4.5                 # P-45..48 lệch vị trí hạt, biên độ đổi cỡ hốc, biên độ đổi độ sâu hốc, tần số nhiễu trên mặt quả (≈ 1 ô nhiễu mỗi hạt) — CHỌN
def bumped_v(q, nw, ph, al, a, amt, sk):   # [F-25]
    """Pháp tuyến có lỗ hạt: hốc P = S((θ − T)/0,25) quanh tâm hạt của lưới lục giác lệch; mỗi hạt lệch chỗ, to nhỏ (θ) và sâu nông (dep) khác nhau theo hai nhiễu giá trị n₁, n₂ trên ζ (seed theo sid sk của quả); gradient hốc bằng sai phân (ε = 0,02 trong hệ ζ)."""
    zeta = surf(q, ph); zeta = zeta + WARP * (M.cos(11.0 * M.real(zeta) + 3.0 * al) + 1j * M.sin(9.0 * M.imag(zeta) + 2.0 * al))
    n1, n2 = value_noise(M.real(zeta), M.imag(zeta), SNF, 3 * sk + 40), value_noise(M.real(zeta), M.imag(zeta), SNF, 3 * sk + 41)
    zeta = zeta + SJIT * (M.cos(2.0 * M.pi * n1) + 1j * M.sin(2.0 * M.pi * n2))                 # hạt lệch khỏi nút lưới
    th, dep = 0.45 + SSIZ * (2.0 * n1 - 1.0), 1.0 + SDEP * (2.0 * n2 - 1.0)                      # ngưỡng hốc (lớn = hốc nhỏ), độ sâu hốc
    T = hexlat(zeta, a); P = sstep((th - T) / 0.25); e = 0.02
    Px, Py = sstep((th - hexlat(zeta + e, a)) / 0.25), sstep((th - hexlat(zeta + 1j * e, a)) / 0.25)
    g = ((Px - P) + 1j * (Py - P)) * (amt * dep / e) * complex(math.cos(al - ph), math.sin(al - ph))
    nx0, ny0 = M.real(nw), M.imag(nw); nz0 = M.sqrt(M.maximum(1.0 - nx0 * nx0 - ny0 * ny0, 0.0))
    k = 0.02 * nz0; uq, vq = M.real(q), M.imag(q)
    gx = 0.07 * M.cos(6.0 * uq + 2.0 * vq + ph) + 0.05 * M.cos(9.0 * vq - 3.0 * uq + 2.0 * ph)
    gy = 0.07 * M.sin(5.0 * vq - 2.5 * uq + ph) + 0.05 * M.sin(8.0 * uq + 4.0 * vq + 3.0 * ph)
    nx, ny, nz = unit3(nx0 + k * M.real(g) + gx * nz0, ny0 + k * M.imag(g) + gy * nz0, nz0)
    return nx, ny, nz, nz0, T, P * dep, zeta, th
def pr_berry_v(z, i, edge=None, box_e=None, detail=1.0):   # [F-26]
    """Quả i kiểu ảnh chụp, dáng riêng (GEO = berry_v) và hạt riêng (bumped_v): thịt quả có lỗ hạt, hạt vàng nhô to nhỏ theo cùng ngưỡng với hốc, phản xạ softbox + môi trường."""
    sd, q, nw = GEO(z, i); c, R, al, ep, ph = POSE[i]
    nx, ny, nz, nz0, T, P, zeta, th = bumped_v(q, nw, ph, al, A_SEED, BUMP * detail, Q[i][3])
    P = P * detail; tip = complex(math.cos(ph - math.pi / 2), math.sin(ph - math.pi / 2))
    seed = sstep((0.86 + 0.5 * (th - 0.45) - hexlat(zeta - 0.025 * tip, A_SEED)) / 0.06) * (0.25 + 0.75 * detail)
    mot = 0.9 + 0.2 * (0.5 + 0.5 * M.cos(5.0 * M.real(q) + 3.0 * M.imag(q) + 1.3 * ph) * M.cos(4.0 * M.imag(q) - 2.0 * M.real(q) + ph))
    alb = tuple(ALB[v] * mot for v in range(3)); so = 0.5 + 0.5 * M.cos(7.0 * M.real(zeta) + 5.0 * M.imag(zeta) + Q[i][3])
    body = shade_flesh(nx, ny, nz, nz0, P, alb)
    nl0 = M.maximum(M.real(nw) * LIGHT[0] + M.imag(nw) * LIGHT[1] + nz0 * LIGHT[2], 0.0)
    sa = tuple(ALB_SEED[v] * (1.0 - 0.45 * so) + ALB[v] * 0.6 * so for v in range(3))
    sk = tuple(sa[v] * (KEY[v] * (0.25 + 0.75 * nl0) + AMBI) * (0.45 + 0.55 * nz0) for v in range(3))
    sp, box = spec(nx, ny, nz, box_e)
    return sd, R, tuple(body[v] * (1.0 - seed) + sk[v] * seed + sp for v in range(3)), q, (nx, ny, nz)
def berry_dof(z, i, edge):   # [F-27]
    """O: quả i với chi tiết giảm và phản chiếu nở mềm theo mức mất nét GB[i]."""
    return pr_berry_v(z, i, edge, box_e=BOXE + 0.3 * GB[i], detail=1.0 - DOFD * GB[i])
def scene(x, y, A, px):   # [F-28]
    """O Macro tiêu điểm: độ sâu trường ảnh bằng độ mềm biên + mất chi tiết; tối góc ống kính; hạt ảnh."""
    z = x + 1j * y; EDGE = 0.75 * px
    H = fold_over(pr_ground(z), pr_layers(z, EDGE, berry_dof, lambda kind, i: DOFB * (GB[i] if kind == 0 else GD[i])))   # L01 nền
    vg = vignette(x, y, VIG); gr = grain(x, y, GRAIN_A)
    return tuple(c + gr for c in encode(tuple(h * vg for h in H)))
# ===== HẾT CÔNG THỨC =====
# ---------- Kết xuất & kiểm chứng (Fidelity B + Test A của Một Công Thức) ----------
def render_tiles(scene_fn, W, H, ss=1, T=8):
    """Như render_of của OF-KIT nhưng gọi scene_fn trên từng ô T×T và đặt VIEW để scene bỏ qua lớp có mặt nạ bằng 0 tuyệt đối trong ô.
    Cho cùng từng bit với render_of(scene_fn, W, H, ss) (đã kiểm ở 1108 × 1108); chỉ nhanh hơn."""
    global VIEW
    acc = None
    with np.errstate(over='ignore'):
        for j in range(ss):
            for i in range(ss):
                x, y, A, px = sample_grid(W, H, ss, i, j); img = np.empty((H, W, 3))
                for r in np.array_split(np.arange(H), T):
                    for c in np.array_split(np.arange(W), T):
                        xt, yt = x[r[0]:r[-1] + 1, c[0]:c[-1] + 1], y[r[0]:r[-1] + 1, c[0]:c[-1] + 1]
                        VIEW = (xt.min(), xt.max(), yt.min(), yt.max())
                        Ht = scene_fn(xt, yt, A, px)
                        img[r[0]:r[-1] + 1, c[0]:c[-1] + 1] = np.stack([np.broadcast_to(np.asarray(h, dtype=np.float64), xt.shape) for h in Ht], axis=-1)
                VIEW = None
                acc = img if acc is None else acc + img
    return acc / float(ss * ss)

u8 = to_uint8(render_tiles(scene, W, H, SS))
save_png(OUT, u8)
EXPECTED_PROBES = [  # (m, n, R, G, B) tại 1108×1108, SS=2 — dung sai ±2/kênh
    (549, 494, 207, 30, 19),   # thịt quả lớn nhất (giữa) — (-0.008, 0.107)
    (201, 279, 213, 31, 20),   # thịt quả trên-trái — (-0.636, 0.495)
    (263, 601, 208, 29, 18),   # thịt quả trái-giữa — (-0.524, -0.086)
    (552, 225, 204, 29, 18),   # thịt quả trên-giữa — (-0.003, 0.593)
    (832, 653, 214, 32, 21),   # thịt quả phải-giữa — (0.503, -0.180)
    (990, 392, 211, 31, 20),   # thịt quả phải — (0.788, 0.292)
    (721, 207, 136, 151, 68),   # gần tâm đài lá trên-phải — (0.302, 0.625)
    (3, 446, 39, 8, 5),   # khe tối – trái — (-0.994, 0.194)
    (735, 308, 50, 9, 7),   # khe tối – giữa — (0.328, 0.443)
    (1104, 1104, 29, 6, 4),   # khe tối – phải — (0.994, -0.994)
    (27, 29, 178, 30, 22),   # góc trên trái — (-0.950, 0.947)
    (1099, 1097, 29, 6, 3),   # góc dưới phải — (0.985, -0.981)
    (554, 445, 252, 197, 195),   # vùng sáng nhất (lấp lánh) — (0.001, 0.196)
    (458, 676, 6, 0, 0),   # vùng tối nhất (khe) — (-0.172, -0.221)
]
EXPECTED_PIXEL_SHA256 = "3710e8ecd15e3374fd93ca4d422df7cdc2f2136791747505130b955a7486076c"
ok_probes = check_probes(u8, EXPECTED_PROBES, tol=2)
ok_hash = check_hash(u8, EXPECTED_PIXEL_SHA256)
ok_point = check_pointwise(scene, u8, W, H, SS, n=100, tol=1)
print("mean RGB:", np.round(u8.reshape(-1, 3).mean(axis=0), 1), "| expected ≈ [147.5 41.7 29.7]")
print("ALL PROBES PASS" if ok_probes else "PROBE MISMATCH — báo cáo, không tự sửa ảnh")
print("REPLAY OK" if (ok_probes and ok_hash and ok_point) else "REPLAY MISMATCH — báo cáo môi trường, không sửa spec")
```

## 6. Dữ liệu kiểm chứng

| m | n | R | G | B | Vị trí (x; y) |
|---|---|---|---|---|---|
| 549 | 494 | 207 | 30 | 19 | thịt quả lớn nhất (giữa) (-0.008; 0.107) |
| 201 | 279 | 213 | 31 | 20 | thịt quả trên-trái (-0.636; 0.495) |
| 263 | 601 | 208 | 29 | 18 | thịt quả trái-giữa (-0.524; -0.086) |
| 552 | 225 | 204 | 29 | 18 | thịt quả trên-giữa (-0.003; 0.593) |
| 832 | 653 | 214 | 32 | 21 | thịt quả phải-giữa (0.503; -0.180) |
| 990 | 392 | 211 | 31 | 20 | thịt quả phải (0.788; 0.292) |
| 721 | 207 | 136 | 151 | 68 | gần tâm đài lá trên-phải (0.302; 0.625) |
| 3 | 446 | 39 | 8 | 5 | khe tối – trái (-0.994; 0.194) |
| 735 | 308 | 50 | 9 | 7 | khe tối – giữa (0.328; 0.443) |
| 1104 | 1104 | 29 | 6 | 4 | khe tối – phải (0.994; -0.994) |
| 27 | 29 | 178 | 30 | 22 | góc trên trái (-0.950; 0.947) |
| 1099 | 1097 | 29 | 6 | 3 | góc dưới phải (0.985; -0.981) |
| 554 | 445 | 252 | 197 | 195 | vùng sáng nhất (lấp lánh) (0.001; 0.196) |
| 458 | 676 | 6 | 0 | 0 | vùng tối nhất (khe) (-0.172; -0.221) |

Mean RGB toàn ảnh [147.5, 41.7, 29.7]. Góc phần tư: TL [163.7, 40.6, 31.3], TR [143.7, 40.7, 29.3], BL [146.7, 45.2, 29.7], BR [135.7, 40.3, 28.6]. Dung sai ±2 mỗi kênh. Mọi probe chọn ở vùng phẳng: lệch lớn nhất trong ô 7 × 7 quanh probe ≤ 5.

EXPECTED_PIXEL_SHA256 = `3710e8ecd15e3374fd93ca4d422df7cdc2f2136791747505130b955a7486076c`
CODE_SHA256 = `093fed4f0aa407b54d935699a702b1fd0fe0533d344ba8f81a647d7262b13540`

Số đo công thức (measure_formula, giữa hai dòng mốc): 11489 ký tự, 663 hằng số, 207 dòng, 27 hàm phụ riêng, render chuẩn ≈ 42.3 s.

| Kiểm thử | Trạng thái |
|---|---|
| Khớp toán–code: ID F-xx ở mục 4.2 = ID trong code (28 ID) | PASS |
| Khớp số toán–code (các hàm lõi triển khai lại bằng cmath từ văn bản mục 4.2, 2 điểm, `work/math_check.py`) | PASS (11 hàm, sai khác lớn nhất 1.1e-16) |
| Probe 14/14, hash pixel | PASS |
| Test A POINTWISE 100 pixel (backend math/cmath) | PASS (100/100) |
| Clean-room, hai tiến trình (R1) | PASS → cấp R1 |
| Tính theo ô == render_of toàn ảnh ở 1108 × 1108 | PASS |
| Chuỗi cấm trong code (ImageDraw, np.random, random., cv2., convolve, blur, Image.open, urllib, requests, subprocess); phần công thức không gọi np.* | PASS |
| Perturbation 4 thay đổi (mục 8) | PASS — bỏ quả, RS: probe ở đúng chỗ bị ảnh hưởng FAIL; dáng, hạt: không probe nào nằm ở chỗ đổi (tác động của nhóm hạt chứng minh bằng phép kiểm từng bit); thước phụ của phép dáng ngược kỳ vọng, đã giải thích bằng phép đo thêm (mục 8) |
| Môi trường thứ hai (R2/R3) | NOT_RUN |

## 7. Mô tả có cấu trúc cho model sinh ảnh (bậc xấp xỉ)

Viết từ render chuẩn của spec này.

```text
Aspect ratio 1:1. A dense pile of 21 ripe strawberries fills the whole frame, seen from above; no table, bowl or background visible.
Largest berries (positions as % from left / % from top): berry centred 50% from left, 43% from top, about 37% of image height across; berry centred 18% from left, 26% from top, about 35% of image height across; berry centred 23% from left, 55% from top, about 32% of image height across; berry centred 50% from left, 20% from top, about 31% of image height across; berry centred 36% from left, 85% from top, about 29% of image height across; berry centred 76% from left, 61% from top, about 28% of image height across. Fifteen smaller berries fill the rest; dark gaps between berries cover about 15% of the image.
Berries are heart/cone shaped with the tip pointing away from their green calyx. Light comes softly from the upper left.
Fourteen green calyx clusters; the five largest at 70% / 73%; 66% / 19%; 31% / 68%; 6% / 90%; 3% / 56%.
Palette: #6E1013, #AF221B, #DF2212, #2F0E09, #ECD3BD, #9CAD4F, #6D6026, #C9A553.
Photorealistic macro photograph, shallow depth of field: the large central berry and its neighbours are sharp, berries further away become progressively soft and lose seed detail, their highlights bloom softly; slight lens vignetting and fine monochrome grain. Glossy red strawberries with softbox reflections, seeds in pits, green lance-shaped sepals. Each berry has its own slightly irregular, lopsided outline; seeds sit slightly irregularly, with pits of varying size and depth.
Style: procedural, anti-aliased edges, no text, no watermark, no people, no other objects.
```

## 8. Báo cáo

**Ràng buộc cứng (T1)**

| # | Ràng buộc | Trạng thái | Bằng chứng |
|---|---|---|---|
| H1 | dâu tây chín đỏ, nhận ra ở thumbnail 240 px | PASS | xem ở 240 px trong cả bốn vòng chấm (`review/judging_log.md`) |
| H2 | đống quả đầy khung, không có nền trống hay vật khác | PASS | 21 quả theo bảng neo phủ khung; khe là quả chìm trong tối |
| H3 | ≥ 15 quả nhìn thấy | PASS | 21 quả có phần nhìn thấy ≥ 0,1% khung (đếm lớp trên cùng ở 554 px) |
| H4 | ≥ 6 cụm đài lá | PASS | 14 đài lá có phần nhìn thấy ≥ 0,03% khung |
| H5 | khung 1:1 | PASS | 1108 × 1108 |
| H6 | không chữ, không người, không vật khác | PASS | công thức không có thành phần nào ngoài quả, đài lá, khe |

**Tương đồng (T2) và bề mặt (T3)**

| Lớp | Nội dung | Kết quả |
|---|---|---|
| T1 Ngữ nghĩa | dâu chín, đống đầy khung, đài lá rải | PASS (bảng trên) |
| T2 Cấu trúc | vị trí và cỡ 21 quả + 14 đài lá đo từ nguồn; hướng sáng đo; palette đo | `lum12` 0.634 ∈ [0,30; 0,85]; ΔE palette 7.2 ≤ 10; `edge_corr` 0.175 (chỉ báo cáo) → PASS |
| T3 Bề mặt | PBR + bump + độ sâu trường ảnh + dáng riêng từng quả, hạt lệch; độ sâu trường ảnh, hạt ảnh | tự do (không lấy texture của nguồn) |

Kết luận bằng mắt: nhận ra ảnh tham chiếu (đống dâu đầy khung, quả lớn nhất ở giữa hơi lệch trên, đài lá xanh ở trên-phải và rải rác, sáng từ trên-trái), không nhầm là bản sao vì bề mặt được vẽ lại hoàn toàn (tả thực quang học).

**Xếp hạng so cặp**: v1.0: lô ảnh chụp p0 1/6, p1 1/5, p2 1/5; Henry chọn. Vòng đánh bóng (so cặp mù, ba cỡ): bước dáng — SHP 0,045 thắng SHP 0,07 và v1.0; bước hạt — mức vừa thắng mức mạnh và lưới đều; chung kết v1.0 ↔ v1.1 — v1.1 thắng. Ở thumbnail hai bản gần như trùng (dhash lệch 1 bit); ở 100% v1.1 bớt vẻ dập cùng một khuôn: quả giữa lệch vai, hốc hạt to nhỏ khác nhau. Mức mạnh của cả hai bước đều thua mức vừa: méo 0,07 làm vài quả có mặt phẳng như bị ép; hạt lệch mạnh tạo hốc to giống vết bệnh.

**Perturbation test** (kỳ vọng ghi trước khi chạy; probe tính lại bằng backend vô hướng tại đúng vị trí probe; thước đo phụ ở 480 px)

| Nhóm | Thay đổi | Kỳ vọng | Quan sát |
|---|---|---|---|
| tắt một object | bỏ quả trên-trái (dòng 19 của Q, sid 19); quả tiêu điểm tìm theo sid = FOCS nên giữ nguyên | probe 'thịt quả trên-trái' FAIL (lộ quả/khe phía sau); quả tiêu điểm, 2 góc, khe phải PASS | probe FAIL: thịt quả trên-trái |
| đổi kích thước | RS 1,1 → 1,0 (mọi quả nhỏ đi 9%) | tỷ lệ pixel khe tối (độ sáng < 0,12) TĂNG; tâm quả không đổi màu vì q = 0 tại tâm bất kể R | probe FAIL: khe tối – giữa, góc trên trái, vùng tối nhất (khe); tỷ lệ khe tối (L < 0,12): 0.0989 → 0.157 Probe khe và góc đổi vì khe rộng ra — cùng hướng kỳ vọng. |
| đổi tham số hạt | SJIT = SSIZ = SDEP = 0 (hạt về lưới đều của v1.0) | chỉ pixel quanh hốc và hạt đổi; khe, góc, đài lá PASS; probe thịt quả PASS nếu ở cả hai bản đều nằm giữa các hốc, FAIL nếu một hốc dời tới; ảnh khi đó trùng từng bit với bản chỉ có dáng riêng (bước 1 của vòng đánh bóng) | probe FAIL: không có Không probe nào FAIL (các probe thịt quả nằm giữa các hốc ở cả hai bản). Bằng chứng tác động của nhóm tham số này là phép kiểm từng bit: SJIT = SSIZ = SDEP = 0 cho ảnh trùng hash với bản chỉ có dáng riêng (200 px), và so mù ở 100% (judging log). |
| đổi tham số dáng | SHP 0,045 → 0 (mọi quả về dáng chung của v1.0) | mép quả dời ≤ 8,5% bán kính (tính từ bảng SHAPE); tâm quả không dời. Diện tích quả ∝ 1 + ½·Σa_k² nên bỏ méo làm quả nhỏ đi rất ít → tỷ lệ khe tối (L < 0,12) TĂNG rất nhẹ; khe ở xa mép và hai góc PASS; probe thịt quả có thể FAIL vì toạ độ q trong quả dãn theo r(θ) (lưới hạt dời theo) | probe FAIL: không có; tỷ lệ khe tối (L < 0,12): 0.0989 → 0.0973 Ngược kỳ vọng ở thước phụ: tỷ lệ L < 0,12 GIẢM nhẹ. Đo thêm (554 px, sau khi chạy): tổng diện tích các quả giảm đúng như dự đoán (0,9803 → 0,9764 khung) nhưng diện tích phủ hợp không đổi (0,8505 → 0,8505) vì phần mép đổi nằm dưới quả khác; khe không rộng ra, thay đổi của thước đến từ vùng tối trên quả và bóng đổ. Kỳ vọng giữ nguyên như đã ghi trước khi chạy. Không probe nào FAIL: probe thịt quả gần tâm, nơi toạ độ q đổi ít nhất. |

Mọi thay đổi đã hoàn tác; spec giữ tham số chuẩn.

**Chọn khi muốn…** muốn bức giống một tấm ảnh macro chụp bằng máy ảnh nhất: có tiêu điểm, có chiều sâu, có hạt.

**Chỉ số phụ trợ** (không xếp hạng bằng chỉ số): clip 0.42%, p5–p95 0.045–0.523, bão hoà 0.789, entropy sắc độ 0.55, mật độ biên 0.029, cân bằng góc phần tư 0.03, lệch tiêu điểm 0.219.

## 9. Nút điều chỉnh

- FOCI (quả tiêu điểm), SHARP (bán kính vùng nét), DOFB, DOFD: độ sâu trường ảnh.
- GRAIN_A, VIG: hạt ảnh và tối góc.
- SHP (P-44): biên độ méo dáng riêng; 0 = dáng chung của v1.0 (mọi quả cùng một khuôn).
- SJIT, SSIZ, SDEP (P-45..47): lệch vị trí, đổi cỡ, đổi độ sâu hốc hạt; cả ba bằng 0 → hạt như v1.0 (lưới đều). SNF (P-48): tần số nhiễu hạt (≈ số ô nhiễu mỗi đơn vị ζ).
- Bảng neo Q, DL (P-01, P-02): vị trí và cỡ quả, đài lá; bỏ một dòng Q là bỏ một quả (thứ tự dòng = thứ tự lớp).
- LIGHT (P-03): hướng sáng; đổi sẽ đổi toàn bộ bóng, lấp lánh và lưỡi liềm.
- RS (P-12): độ đầy của đống quả (bán kính dáng / bán kính đo).
- Palette K_* (P-04…P-11): sáu màu đo của nguồn; đổi màu giữ nguyên hình.
- Độ phân giải: đổi W = H (giữ 1:1); mọi hình giữ nguyên vì toạ độ chuẩn hoá; probe và hash chỉ đúng ở 1108 × 1108, SS = 2.
- Tạo biến thể giữ "điểm phải giữ" (tiêu điểm rõ, quả xa mềm dần, hạt ảnh (giữ nguyên từ v1.0)): đổi tham số ở mục 4.3 của bức này, không đổi bảng neo nếu muốn giữ độ tương đồng bậc 2; mỗi biến thể là spec mới (tăng minor, sinh lại probe và hash).

## 10. Changelog

- Dựng: lõi PBR chung (xem N).
- p1: cánh đài hình mác đầy, mũi nhọn (sửa chung cả lô) — giữ.
- p2: vùng nét SHARP = 0,35 quanh quả tiêu điểm — giữ.
- v1.0 — 06/10/2026: đóng gói; làm sạch (tỉa hàm không dùng ở lõi chung và lõi PBR, đánh lại ID) — pixel ở 480 px trùng bản p2.
- v1.0 — 06/10/2026: Henry chọn (ACCEPTED). Giữ nguyên ở final/dong-dau-tay_spec_v1.md.
- v1.1 — 06/10/2026: vòng đánh bóng (đề nghị của Claude Code, Henry đồng ý: "Hãy làm 1 vòng đánh bóng như bạn suggest"). (1) Dáng riêng từng quả: berry_v, _shape, SHP = 0,045 (bước 1; so mù với SHP 0,07 và v1.0). (2) Hạt bớt trật tự: bumped_v, pr_berry_v, SJIT 0,02, SSIZ 0,08, SDEP 0,3, SNF 4,5 (bước 2; so mù với mức mạnh 0,035/0,14/0,5 và với bước 1). Kiểm: SJIT = SSIZ = SDEP = 0 cho ảnh trùng từng bit với bước 1 (200 px). Mọi tham số khác, bảng neo, ánh sáng, độ sâu trường ảnh giữ nguyên; bump/pr_berry của lõi PBR không còn dùng nên đã tỉa.
