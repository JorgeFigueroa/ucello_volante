## Inizia un progetto web
npm init -y

# Installa Capacitor
npm install @capacitor/core @capacitor/cli

# Inizializza Capacitor
npx cap init

# crea cartela webDir
mkdir www

# Installa la piattaforma Android di Capacitor
npm install @capacitor/android

# npx cap add android
npx cap add android

# verificare versioni installate
npm list @capacitor/android

# Apri Android Studio - non funziona da errore no trova android varibile CAPACITOR_ANDROID_STUDIO_PATH
npx cap open android


# Sincronizza Capacitor 
npx cap sync

# copiare i file web aggiornati dentro /android
npx cap copy android


# Installa un server statico:
npm install -g serve
serve .