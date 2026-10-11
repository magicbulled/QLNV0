# Sơ đồ lớp - Hệ thống Đăng ký Học phần

![Sơ đồ lớp](dang_ky_hoc_phan.png)

## Mô tả quan hệ

| Quan hệ | Loại | Bội số |
|---|---|---|
| MonHoc - LopHocPhan | Hợp thành (composition) | 1 - 0..* |
| GiangVien - LopHocPhan | Kết hợp (association) | 1 - 0..* |
| SinhVien - PhieuGhiDanh | Kết hợp | 1 - 1..* |
| LopHocPhan - PhieuGhiDanh | Kết hợp | 1 - 0..* |
| PhieuGhiDanh - TrangThaiGhiDanh | Phụ thuộc (dependency) | - |

Xóa một `MonHoc` thì toàn bộ `LopHocPhan` thuộc môn đó bị xóa theo.

## Mã PlantUML

```plantuml
@startuml DangKyHocPhan
title Sơ đồ lớp - Hệ thống Đăng ký Học phần

skinparam classAttributeIconSize 0
skinparam linetype ortho

enum TrangThaiGhiDanh {
  CHO_DUYET
  DA_DUYET
  DA_HUY
}

class SinhVien {
  - maSV : String
  - hoTen : String
  - email : String
  + dangKy(lop : LopHocPhan) : PhieuGhiDanh
  + huyDangKy(phieu : PhieuGhiDanh) : void
}

class GiangVien {
  - maGV : String
  - hocVi : String
}

class MonHoc {
  - maMon : String
  - tenMon : String
  - soTinChi : int
}

class LopHocPhan {
  - maLop : String
  - siSoToiDa : int
  - phongHoc : String
}

class PhieuGhiDanh {
  - ngayDangKy : Date
  - trangThai : TrangThaiGhiDanh
  - diemTongKet : float
}

' Môn học sở hữu chặt chẽ Lớp học phần (xóa môn -> xóa lớp)
MonHoc "1" *-- "0..*" LopHocPhan : gồm >

' Giảng viên phụ trách Lớp học phần
GiangVien "1" -- "0..*" LopHocPhan : phụ trách >

' Ghi danh
SinhVien "1" -- "1..*" PhieuGhiDanh : có >
LopHocPhan "1" -- "0..*" PhieuGhiDanh : có >

PhieuGhiDanh ..> TrangThaiGhiDanh

@enduml
```
