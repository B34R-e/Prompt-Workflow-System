# Simple Agentic Documentation Framework 🤖

Welcome to the **Agentic Documentation Framework**. This is a documentation structure designed specifically for projects that rely heavily on AI Agents (like GitHub Copilot, Cursor, Codeium, or custom LLM scripts) for pair-programming and development.
*(Kéo xuống dưới để xem bản Tiếng Việt 🇻🇳)*

Unlike traditional wikis meant for human readers, this framework serves as an **Operating System for AI Agents**. It clearly separates instructions (prompt engineering) from data (project specifications), uses a gated pipeline to prevent hallucinations, and dynamically scales based on project size.

## 🌟 Why use this framework?

1.  **Prevents Hallucinations:** Prevents the AI from making wild assumptions by forcing it to read strict localized rules and maintain a clear separation between "Assumptions" and "Unknowns".
2.  **State Management for AI:** Uses a "Living Changelog" and "Feature Tracker" instead of raw Git history, giving the AI a clean context of what is currently active without confusing it with dead-end code refactors.
3.  **Context Optimization:** Dynamically loads rules (like testing, coding conventions, or security audits) only when the project scale demands it, keeping the context window lean for smaller PoC/Spike projects.
4.  **Enforces "Definition of Ready" (DoR):** The AI cannot jump into coding without first satisfying the prerequisites defined in the early stages (Scope → Problem → Requirements → Architecture → Detailed Design).

## 📁 Folder Structure

The framework is organized into two groups:

### Meta (Framework tooling — not SDLC phases)
*   **`_meta/Identify/`**: Trigger questions per SDLC phase (written in English).
*   **`_meta/Checklist/`**: Validation checklists for requirements and architecture quality.
*   **`_meta/Rules/`**: The routing engine, grounding rules, task-type modules, and extensions.
    *   *Note on `_meta/Rules/extensions/`: Contains specialized rules (like strict coding conventions, testing requirements) that are dynamically loaded for MVP or Production scale projects.*
*   **`_meta/README/`**: Contains instructions for using this framework.

### SDLC Phases (Sequential, top-down)
*   **`01_Project_Scope/`**: Project scope output (written in your native language).
*   **`02_Problem_Definition/`**: Problem definition output.
*   **`03_Requirements/`**: Functional and non-functional requirements.
*   **`04_Architecture/`**: High-Level Design (HLD) — major blocks, interfaces, deployment.
*   **`05_Detailed_Design/`**: Per-Major-Block detailed design — classes, methods, data flow. Bridges HLD → Implementation.
*   **`06_Research/`**: Scratchpads for the AI to conduct deep dives (includes `analysis/` subfolder).
*   **`07_Features/`**: Trackers for specific functional areas (e.g., Auth, Chat, Payments).
*   **`08_Business_Flow/`**: Business flow documentation (process diagrams, user journeys).
*   **`09_Changes_History/`**: The "Living Changelog" where the AI records active modifications.
*   **`10_Common/`**: Shared reference files (API, Database, UI/UX, Security, Testing).
*   **`11_Environment/`**: Onboarding, setup scripts, deployment guides, and project Runbook (A-Z reproduction guide) for human developers.

## 🚀 How to Get Started

To understand how to interact with the AI using this framework, please read:
👉 **[_meta/README/How_to_use.md](./_meta/README/How_to_use.md)**

**Basic Usage Summary:**
1. Tell your AI Agent: *"Please read `agent_framework/_meta/Rules/Agent_Rules.md` and act as my pair-programmer."*
2. Follow the initialization steps to generate the SDLC phase files (01 → 02 → 03 → 04 → 05).
3. For daily work, simply give the Agent a task. The routing engine in `Agent_Rules.md` will automatically guide it to use the correct sub-modules (Planning, Execution, Bug Triage, etc.).

## 📝 Disclaimer & References

**Disclaimer:** This framework is built upon my personal experiences, knowledge, and practical lessons learned from developing solo and team projects alongside AI Agents. It is a highly opinionated workflow and may need further tuning for your specific use cases.

**References:**
The concepts and architectural hygiene enforced by this framework were heavily inspired by the following books:
- *Code Complete (2nd Edition)* by Steve McConnell

---
---

# 🇻🇳 Khung Tài Liệu Dành Cho AI Agent (Agentic Documentation Framework)

Chào mừng bạn đến với **Agentic Documentation Framework**. Đây là một cấu trúc tài liệu được thiết kế đặc biệt cho các dự án phụ thuộc nhiều vào AI Agents (như GitHub Copilot, Cursor, Codeium, hay các LLM script tự viết) để lập trình cặp (pair-programming).

Khác với các dạng Wiki truyền thống dành cho người đọc, framework này đóng vai trò như một **"Hệ Điều Hành" dành cho AI Agents**. Nó phân định rõ ràng giữa Hướng dẫn/Prompt và Dữ liệu/Nội dung dự án, sử dụng một quy trình có cổng chặn (gated pipeline) để chống ảo giác, đồng thời tự động co giãn linh hoạt theo quy mô dự án.

## 🌟 Tại sao nên dùng framework này?

1.  **Chống Ảo Giác (Prevents Hallucinations):** Ngăn AI tự đưa ra các giả định hoang đường bằng cách ép buộc nó đọc các bộ nguyên tắc cục bộ cực kỳ nghiêm ngặt, rạch ròi giữa "Assumption" (Giả định) và "Unknown" (Chưa rõ).
2.  **Quản Lý Trạng Thái Cho AI (State Management):** Sử dụng "Living Changelog" và "Feature Tracker" thay vì Git history thô. Điều này giúp AI có bức tranh về ngữ cảnh hiện tại một cách gọn gàng, không bị nhiễu bởi các "ngõ cụt" (dead-ends) khi refactor code.
3.  **Tối Ưu Hóa Ngữ Cảnh (Context Optimization):** Tự động nạp các bộ rule (như viết test, coding convention, hay audit bảo mật) CHỈ KHI quy mô dự án yêu cầu, giúp bảo toàn dung lượng Context Window cho các dự án PoC/Spike nhỏ gọn.
4.  **Ép Buộc Chuẩn Mực (Definition of Ready - DoR):** AI không thể nhảy ngay vào việc viết code nếu chưa thỏa mãn các điều kiện tiên quyết (Prerequisites) được định nghĩa ở các bước đầu (Phạm vi → Vấn đề → Yêu cầu → Kiến trúc → Thiết kế chi tiết).

## 📁 Cấu Trúc Thư Mục

Khung tài liệu được tổ chức thành hai nhóm:

### Meta (Công cụ framework — không phải SDLC phases)
*   **`_meta/Identify/`**: Câu hỏi kích hoạt cho từng phase SDLC (viết bằng tiếng Anh).
*   **`_meta/Checklist/`**: Danh sách kiểm tra chất lượng cho requirements và architecture.
*   **`_meta/Rules/`**: Engine định tuyến, quy tắc grounding, modules theo loại task, và extensions.
    *   *Lưu ý về `_meta/Rules/extensions/`: Chứa các bộ rule chuyên sâu được AI tự động nạp linh hoạt riêng cho các dự án quy mô MVP hoặc Production.*
*   **`_meta/README/`**: Hướng dẫn sử dụng framework.

### SDLC Phases (Tuần tự, top-down)
*   **`01_Project_Scope/`**: Đầu ra phạm vi dự án (viết bằng ngôn ngữ mẹ đẻ).
*   **`02_Problem_Definition/`**: Đầu ra định nghĩa vấn đề.
*   **`03_Requirements/`**: Yêu cầu chức năng và phi chức năng.
*   **`04_Architecture/`**: Thiết kế tổng thể (HLD) — major blocks, interfaces, deployment.
*   **`05_Detailed_Design/`**: Thiết kế chi tiết từng Major Block — classes, methods, data flow. Cầu nối HLD → Implementation.
*   **`06_Research/`**: Nơi AI nghiên cứu/phân tích sâu (bao gồm `analysis/` subfolder).
*   **`07_Features/`**: Tracker theo dõi trạng thái các nhóm tính năng (ví dụ: Auth, Chat, Payments).
*   **`08_Business_Flow/`**: Tài liệu luồng nghiệp vụ (sơ đồ quy trình, user journeys).
*   **`09_Changes_History/`**: "Living Changelog" — nơi AI ghi lại lịch sử biến đổi đang active.
*   **`10_Common/`**: Các file tham chiếu dùng chung (API, Database, UI/UX, Security, Testing).
*   **`11_Environment/`**: Onboarding, setup, deployment guides, và Runbook dự án (hướng dẫn reproduce A-Z) cho lập trình viên.

## 🚀 Hướng Dẫn Bắt Đầu

Để hiểu cách tương tác với AI khi sử dụng framework này, vui lòng đọc:
👉 **[_meta/README/How_to_use.md](./_meta/README/How_to_use.md)**

**Tóm Tắt Cách Dùng Nhanh:**
1. Hãy ra lệnh cho AI Agent của bạn: *"Please read `agent_framework/_meta/Rules/Agent_Rules.md` and act as my pair-programmer."*
2. Làm theo các bước khởi tạo (initialization) để cùng AI sinh ra các file SDLC phase (01 → 02 → 03 → 04 → 05).
3. Trong công việc hàng ngày, bạn chỉ việc giao task bình thường. AI engine trong `Agent_Rules.md` sẽ tự động định tuyến để sử dụng đúng các sub-modules (Planning, Execution, Bug Triage, v.v.).

## 📝 Lời Từ Chối Trách Nhiệm (Disclaimer) & Tài Liệu Tham Khảo

**Disclaimer:** Framework này được xây dựng hoàn toàn đúc kết từ những trải nghiệm, kiến thức, và học hỏi cá nhân trong quá trình phát triển các dự án thực tế (cả làm hỏa tốc solo lẫn làm việc với team) khi có sử dụng AI Agents. Đây là một workflow mang nặng tính cá nhân hóa (highly opinionated) và bạn có thể cần điều chỉnh đôi chút cho phù hợp với dự án cụ thể của mình.

**Tài Liệu Tham Khảo:**
Các nguyên lý kiến trúc và tư duy kiểm soát chất lượng phần mềm trong framework này được truyền cảm hứng to lớn từ tựa sách nổi tiếng:
- *Code Complete (2nd Edition)* - Tác giả: Steve McConnell
