# Fotoopowieści — instrukcja wgrania i konfiguracji panelu CMS

## Co dostałeś

```
fotoopowiesci/
├── index.html          ← główna strona
├── admin/
│   ├── index.html      ← panel edycji (wchodzisz na /admin)
│   └── config.yml      ← konfiguracja panelu
└── _data/
    ├── general.json    ← imię, kontakt, teksty hero i "o mnie"
    ├── packages.json   ← pakiety cenowe
    ├── gallery.json    ← zdjęcia w galerii
    └── testimonials.json ← opinie klientów
```

---

## KROK 1 — Wgraj pliki na GitHub

1. Wejdź na github.com → repozytorium `fotoopowiesci`
2. Kliknij **Add file → Upload files**
3. Przeciągnij WSZYSTKIE pliki i foldery z pobranego archiwum:
   - `index.html`
   - folder `admin/` (z dwoma plikami w środku)
   - folder `_data/` (z czterema plikami JSON)
4. Kliknij **Commit changes**

> Jeśli plik `index.html` już istnieje na GitHubie — usuń go najpierw (kliknij na plik → ikonka kosza), a potem wgraj nowy.

---

## KROK 2 — Włącz GitHub OAuth (jednorazowe, 5 minut)

Decap CMS loguje się przez GitHub. Musisz zarejestrować aplikację OAuth:

1. Wejdź na: https://github.com/settings/developers
2. Kliknij **New OAuth App**
3. Wypełnij:
   - **Application name:** `Fotoopowiesci CMS`
   - **Homepage URL:** `https://wojtekgontarz-lang.github.io/fotoopowiesci/`
   - **Authorization callback URL:** `https://api.netlify.com/auth/done`
4. Kliknij **Register application**
5. Skopiuj **Client ID** i kliknij **Generate a new client secret** — skopiuj też secret

---

## KROK 3 — Skonfiguruj Netlify Identity (darmowe)

Netlify służy tu tylko jako pośrednik OAuth — strona nadal hostowana jest na GitHub Pages.

1. Wejdź na: https://app.netlify.com i załóż darmowe konto (możesz się zalogować przez GitHub)
2. Kliknij **Add new site → Import an existing project → GitHub** i wybierz repozytorium `fotoopowiesci`
3. Ustaw: Build command — puste, Publish directory — `/`
4. Kliknij **Deploy site**
5. W ustawieniach nowego site'u w Netlify: **Site configuration → Access control → OAuth** → Add provider → GitHub → wklej Client ID i Client Secret z kroku 2

---

## KROK 4 — Używaj panelu

Po wgraniu wszystkich plików wejdź na:

```
https://wojtekgontarz-lang.github.io/fotoopowiesci/admin/
```

Zaloguj się przez GitHub — i możesz edytować wszystko przez wygodny panel.

---

## Edycja bez panelu (alternatywa)

Jeśli nie chcesz konfigurować OAuth, możesz zawsze edytować pliki JSON bezpośrednio na GitHubie:

- `_data/general.json` — imię, tagline, teksty, e-mail, telefon
- `_data/packages.json` — pakiety cenowe
- `_data/gallery.json` — zdjęcia (linki lub ścieżki do plików)
- `_data/testimonials.json` — opinie

Kliknij plik → ołówek → zmień wartość między cudzysłowami → Commit changes.

---

## Podłączenie formularza kontaktowego

Formularz domyślnie pokazuje tylko potwierdzenie. Żeby działał realnie:

1. Zarejestruj się na https://web3forms.com (darmowy plan: 250 wiadomości/miesiąc)
2. Skopiuj Access Key
3. W `index.html` znajdź `<form class="contact-form"` i zmień na:
   ```html
   <form class="contact-form" action="https://api.web3forms.com/submit" method="POST">
   <input type="hidden" name="access_key" value="TWÓJ_KLUCZ_TUTAJ">
   ```
4. Commit changes — i formularz wysyła maile na Twój adres.
