# SLAPRP.jl – Chuyên đề 2

**Nhóm 15**

**Võ Văn Tín** – 106210254
**Trần Văn Sáng** – 106210051

---

## Giới thiệu

Dự án này triển khai và thực nghiệm bài toán **Gán vị trí lưu trữ và Định tuyến người lấy hàng** (*Storage Location Assignment and Picker Routing Problem – SLAPRP*) trong kho hàng, với mục tiêu **tối thiểu hóa tổng quãng đường di chuyển của người lấy hàng**.

Bài toán SLAPRP là một bài toán tối ưu tổ hợp tích hợp, kết hợp đồng thời:

* **Bài toán gán vị trí lưu trữ (SLAP)**
* **Bài toán định tuyến người lấy hàng (PRP)**

Dự án sử dụng **thuật toán Branch-Cut-and-Price**, dựa trên phân rã **Dantzig–Wolfe**, để giải chính xác các instance SLAPRP có kích thước trung bình, thay vì sử dụng các phương pháp heuristic.

Mã nguồn được xây dựng dựa trên phương pháp được trình bày trong bài báo:

> *The Storage Location Assignment and Picker Routing Problem:
> A Generic Branch-Cut-and-Price Algorithm*
> Thibault Prunet, Nabil Absi, Diego Cattaruzza
> *European Journal of Operational Research (2025)*

---


## Cấu trúc thư mục

```
SLAPRP.jl/
│
├── src/                # Mã nguồn chính (mô hình, pricing, BCP)
├── test/
│   └── main.jl         # File chạy thực nghiệm
│
├── data/               # Dữ liệu đầu vào 
├── result_guo_return.csv           # Kết quả xuất ra (CSV)
│
├── Project.toml        
├── Manifest.toml
└── README.md
```

---

## Yêu cầu hệ thống

* **Julia ≥ 1.6**
* **ILOG CPLEX 20.1** 

Cài đặt CPLEX cho Julia, tham khảo:
[https://github.com/jump-dev/CPLEX.jl](https://github.com/jump-dev/CPLEX.jl)

> ⚠️ Lưu ý: CPLEX yêu cầu giấy phép hợp lệ (academic hoặc commercial).

---

## Hướng dẫn cài đặt

Clone mã nguồn và cài đặt các package cần thiết:

```julia
using Pkg
Pkg.activate(".")
Pkg.instantiate()
```

Sau đó load chương trình:

```julia
include("test/main.jl")
```

---

## Chạy thực nghiệm

Sử dụng hàm:

```julia
run(dataset, policy)
```

### Tham số

* `dataset`:

  * `"silva"`
  * `"guo"`

* `policy` :

  * `"exact"` 
  * `"return"`
  * `"sshape"`
  * `"midpoint"`
  * `"largest"`

⚠️ **Lưu ý**: Với dataset **Guo**, chỉ hỗ trợ chính sách `"return"`.

### Ví dụ

```julia
run("guo", "return")
```

> ⏳ Thời gian chạy có thể lớn do độ phức tạp của thuật toán Branch-Cut-and-Price.

---

## Tài liệu tham khảo

```bibtex
@article{prunet2025storagelocationassignmentpicker,
  title   = {The storage location assignment and picker routing problem: 
             A generic branch-cut-and-price algorithm},
  journal = {European Journal of Operational Research},
  volume  = {327},
  number  = {3},
  pages   = {857--874},
  year    = {2025},
  doi     = {10.1016/j.ejor.2025.05.041},
  author  = {Thibault Prunet and Nabil Absi and Diego Cattaruzza}
}
```
