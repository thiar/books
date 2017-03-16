Table

user
  - id: integer
  - password: string
  - email: string
  - nrp: string
  - -----------------
  - frs() : hasMany

matakuliah
  - id
  - kode: string
  - nama: string
  - kelas: string
  - -----------------
  - frs() : hasMany

frs
  - id: integer
  - user_id: integer
  - matakuliah_id: integer
  - nilai: float
  - -----------------
  - user() : belongsTo
  - matakuliah() : belongsTo
