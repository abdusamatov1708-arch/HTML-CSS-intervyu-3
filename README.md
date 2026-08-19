# HTML-CSS-intervyu-3
position qiymatlari va ularning farqlari
static (Standart): Element sahifaning odatiy oqimida (document flow) joylashadi. Unga top, bottom, left, right va z-index xususiyatlari ta'sir qilmaydi.

relative: Element o'zining normal o'rniga nisbatan siljiydi. Lekin uning avvalgi joyi sahifada bo'sh qoladi. Shuningdek, u ichidagi absolute elementlar uchun "containing block" (tayanch nuqta) vazifasini bajaradi.

absolute: Element sahifadagi normal oqimdan butunlay uzilib chiqadi. U o'zining eng yaqin pozitsiyalangan (relative, absolute, fixed) ota-onasiga nisbatan joylashadi. Agar bunday ota-ona bo'lmasa, sahifa oynasiga (<html>) nisbatan siljiydi.

fixed: Element sahifa oynasiga (viewport) nisbatan qotib qoladi. Sahifani pastga skroll qilganda ham u o'z joyida o'zgarmasdan turadi. Normal oqimdan chiqib ketadi.

sticky: relative va fixed o'rtasidagi gibrid. Element skroll qilish jarayonida o'zining odatiy joyida turadi (relative), lekin belgilangan nuqtaga (top: 0 kabi) yetib borgach, ekranga yopishib qoladi (fixed kabi).
z-index faqat bitta stacking context ichidagigina ishlaydi. Quyidagi xususiyatlardan biri qo'llanilganda yangi stacking context hosil bo'ladi:

Root element (<html>).

position: absolute yoki relative bo'lib, z-index qiymati auto dan farqli bo'lsa.

position: fixed yoki sticky.

opacity qiymati 1 dan kichik bo'lsa (masalan, 0.9).

transform xususiyati none dan farqli bo'lsa (masalan, scale(1) yoki translateY(0)).

filter yoki backdrop-filter ishlatilsa.

display: flex yoki grid ichidagi bolalar, agar ularda z-index auto dan farqli bo'lsa.

isolation: isolate.
z-index Nega Ba'zida Ishlamaydi? (Misollar)
z-index ishlamasligining eng keng tarqalgan 2 ta sababi:

Sabab 1: Element pozitsiyalanmagan (position: static)
z-index faqat position qiymati static bo'lmagan elementlargagina ta'sir qiladi.

CSS
/* XATO: z-index ishlamaydi */
.box {
    z-index: 999;
    /* position sukut bo'yicha static */
}

/* TO'G'RI */
.box {
    position: relative; /* yoki absolute, fixed */
    z-index: 999;
}
Faraz qilaylik, sizda ikkita element bor: .modal va .dropdown.

.modal ning ota-onasida opacity: 0.9 bor (demak, u yangi stacking context yaratgan).

.dropdown ning ota-onasida stacking context yo'q, lekin uning o'zida z-index: 9999 bor.
Agar .modal ichidagi elementga z-index: 1 bersangiz ham, u .dropdown ning ustiga chiqib ketishi mumkin. Chunki .modal o'zining ichki olamini yaratgan va tashqi dunyodagi z-index qoidalariga bo'ysunmaydi.
Qirqish (Clipping): Agar ota elementga overflow: hidden (yoki auto, scroll) berilgan bo'lsa va uning ichidagi bola element position: absolute yordamida tashqariga chiqib ketsa, ota element chegarasidan chiqqan qism ko'rinmay qoladi (kesib tashlanadi).

Containing Block ta'siri: Zamonaviy brauzerlarda ba'zi hollarda overflow xususiyati (agar u visible dan boshqa bo'lsa) o'zi ichidagi absolute elementlar uchun containing block yaratib qo'yishi mumkin.
Containing block — bu boshqa elementning joylashuvi (top, left) va o'lchami (width, height) hisoblanadigan asosiy ota-ona yoki hudud.

position: absolute bo'lgan element uchun containing block quyidagicha aniqlanadi:

Agar ota elementning position qiymati relative, absolute yoki fixed bo'lsa, o'sha ota element containing block bo'ladi.

Agar bunday ota element topilmasa, qidiruv yuqoriga davom etadi va oxir-oqibat <html> (Initial Containing Block) asosiy tayanch bo'lib qoladi.

Sizni ko'proq CSS animatsiyalari va transition xususiyatlari qiziqtiradimi yoki JavaScript yordamida DOM bilan ishlashmi?
