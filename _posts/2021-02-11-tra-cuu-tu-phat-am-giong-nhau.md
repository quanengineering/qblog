---
layout: single
toc: false
title: "Tra cứu các từ phát âm giống hoặc tương tự nhau"
date: 2021-02-19
tags:
  - Ngôn ngữ
  - Công nghệ
lang: vi
---

Trong tiếng Anh, có một số từ có cách phát âm (pronunciation) tương tự nhau, thậm chí là giống nhau hoàn toàn, mặc dù mặt chữ (spelling) và nghĩa (meaning) khác nhau.

Khi gặp các từ đó, mình luôn ngờ ngợ vì cảm giác nó giống từ nào đó đã từng học rồi. Mình có thử sử dụng các [danh sách có sẵn](https://www.home-speech-home.com/minimal-pairs.html) để tra cứu nhưng gặp khó khăn vì không liệt kê đầy đủ. Để có công cụ tra cứu tốt nhất, mình đã dành hai tuần để viết Similar-sounding Words - tiện ích mở rộng (extension) cho trình duyệt Chrome. Các bạn có thể sử dụng [link này](https://chrome.google.com/webstore/detail/similar-sounding-words/hobghciacmpkhkpaidahlcmedkppkbkg) để cài đặt.

Tiện ích này sẽ giúp từ điển [Oxford Advanced Learner](https://www.oxfordlearnersdictionaries.com/definition/english/) hiển thị danh sách các từ có cách phát âm giống hệt với từ đang tra (thuật ngữ chuyên ngành gọi là homophones) và các từ phát âm gần giống từ đang tra, chỉ khác nhau đúng một âm (minimal pairs).

Ví dụ, khi tra từ [flower](https://www.oxfordlearnersdictionaries.com/definition/english/flower_1) (bông hoa), mục Homophones sẽ được tự động thêm vào, hiển thị từ phát âm giống là flour (bột mì). Tương tự cho các cặp từ khác như [Thai](https://www.oxfordlearnersdictionaries.com/definition/english/thai), [tie](https://www.oxfordlearnersdictionaries.com/definition/english/tie_1).

{% include figure image_path="/assets/images/similar-sounding-words-1.png" alt="Các từ phát âm giống từ flower" caption="Các từ phát âm giống từ [flower](https://www.oxfordlearnersdictionaries.com/definition/english/flower_1)" %}

Với một từ khác là [arcane](https://www.oxfordlearnersdictionaries.com/definition/english/arcane), mục Minimal Pairs sẽ hiển thị từ [arcade](https://www.oxfordlearnersdictionaries.com/definition/english/arcade) có phát âm tương tự, chỉ khác nhau âm cuối (âm d và n).

{% include figure image_path="/assets/images/similar-sounding-words-2.png" alt="Các từ phát âm tương tự từ arcane" caption="Các từ phát âm tương tự từ [arcane](https://www.oxfordlearnersdictionaries.com/definition/english/arcane)" %}

Để lọc ra được danh sách các cặp từ này, mình đã tiến hành thu thập toàn bộ ngữ âm (phonetic) của Oxford Advanced Learner's Dictionary và so sánh từng cặp phonetic một cách tự động. Quá trình này sẽ được lặp lại khi Oxford bổ sung từ mới vào từ điển nên các bạn có thể yên tâm về độ chính xác và mức độ cập nhật của Similar-sounding Words.
