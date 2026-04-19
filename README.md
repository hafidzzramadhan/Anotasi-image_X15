ANNOTATION IMAGE 
By : "Hj.Dr.Hafidz ramadhan S.kom

This is my project that i built base on Ai , The purpose of this project is make a model to train Ai so it can be a camera detection or face recognition 
#Step by step to Run it 

# 1. Clone
git clone https://github.com/hafidzzramadhan/Anotasi-image_X15.git
cd Anotasi-image_X15

# 2. Virtual env + install
python3 -m venv .venv
source .venv/bin/activate              # Mac/Linux
# .venv\Scripts\activate               # Windows
pip install -r requirements.txt

# 3. Setup .env dari template
cp .env.example .env (((ADA DI PALING BAWAH TINGGAL COPY-PASTE ))

# 4. Setup PostgreSQL (sekali aja)
createdb anotasi_image
psql -d anotasi_image << 'EOF'
CREATE USER anotasi_user WITH PASSWORD 'password-yang-dia-set-di-.env';
GRANT ALL PRIVILEGES ON DATABASE anotasi_image TO anotasi_user;
GRANT ALL ON SCHEMA public TO anotasi_user;
ALTER DATABASE anotasi_image OWNER TO anotasi_user;
EOF

# 5. Migrate + superuser
python manage.py migrate
python manage.py createsuperuser

# 6. Jalan
python manage.py runserver


Untuk step no 3 (.env.example) -->copy paste aja di bawah

cat > .env.example << 'EOF'
# Django
DJANGO_SECRET_KEY=ganti-dengan-key-random-panjang
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# PostgreSQL
DB_NAME=anotasi_image
DB_USER=anotasi_user
DB_PASSWORD=ganti-password-lu
DB_HOST=localhost
DB_PORT=5432

# Google OAuth (optional — kosongin kalau ga dipake)
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

# AI API
AI_API_URL=https://pursue-various-engineer-corporate.trycloudflare.com/api/proses-gambar/
EOF

git add .env.example
git commit -m "chore: add .env.example template"
git push
