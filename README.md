# Kimi Agent Skills

> Bộ sưu tập skill được tổng hợp từ Kimi Agent, tập trung vào tạo và xử lý tài liệu chuyên nghiệp.

[English](#english) · [Tiếng Việt](#tiếng-việt)

## English

This repository is a curated collection of skills extracted from the Kimi Agent ecosystem. It packages reusable workflows for high-quality document generation and data work so they can be installed and reused by AI coding agents.

### Included skills

| Skill | Purpose |
|---|---|
| `kimi-docx` | Create and edit Word documents with professional layouts, charts, comments, track changes, and OpenXML tooling. |
| `kimi-pdf` | Create PDFs through HTML/Paged.js or LaTeX, and extract, merge, split, or fill existing PDFs. |
| `kimi-xlsx` | Build and manipulate Excel workbooks with formulas, styling, charts, and PivotTables. |

### Install

```bash
npx skills add nstung463/kimi-agent-skills
```

You can also copy an individual skill from `skills/` into the skills directory used by your agent.

### Repository layout

```text
kimi-agent-skills/
├── skills/
│   ├── kimi-docx/
│   ├── kimi-pdf/
│   └── kimi-xlsx/
├── examples/
├── .agent/
└── .agents/
```

### Requirements

- `kimi-docx`: Python 3; .NET SDK and Pandoc are useful for some workflows.
- `kimi-pdf`: Node.js, Playwright, and Python 3.
- `kimi-xlsx`: Python 3 with `openpyxl` and `pandas`.

Individual `SKILL.md` files contain the detailed workflow and dependency notes for each skill.

## Tiếng Việt

Đây là repo tổng hợp các skill có nguồn gốc từ hệ sinh thái Kimi Agent, được đóng gói để có thể cài đặt và tái sử dụng trong các AI coding agent. Repo tập trung vào ba nhóm công việc: Word, PDF và Excel.

### Nguồn gốc và attribution

Các skill ban đầu được phát triển cho Kimi AI Assistant bởi [Moonshot AI](https://www.moonshot.cn/). Repo này là bản tổng hợp/đóng gói cộng đồng, không phải sản phẩm chính thức của Moonshot AI và không đại diện cho Kimi.

Vui lòng xem từng `SKILL.md` và lịch sử nguồn để biết chi tiết. Khi tái phân phối hoặc chỉnh sửa, hãy giữ nguyên thông tin attribution và tôn trọng giấy phép/quyền của tác giả gốc.

### Ví dụ

Thư mục `examples/` chứa các ví dụ đầu ra và script minh họa cho việc tạo tài liệu, PDF và bảng tính.

## Credits

- Original skill ecosystem: [Kimi](https://www.kimi.com/) / [Moonshot AI](https://www.moonshot.cn/)
- Community packaging and documentation: this repository

## License

Hãy xem thông tin giấy phép và attribution trong từng skill trước khi sử dụng cho mục đích thương mại hoặc tái phân phối. Mọi quyền đối với phần triển khai gốc thuộc về chủ sở hữu tương ứng.
