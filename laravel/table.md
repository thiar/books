Table

user
  - id
  - password
  - email
  - nrp
  - role
  ------------------
  - frs() : hasMany

matakuliah
  - id
  - kode
  - nama
  - kelas
  ------------------
  - frs() : hasMany

frs
  - id
  - user_id
  - matakuliah_id
  - nilai
  ------------------
  - user() : belongsTo
  - matakuliah() : belongsTo