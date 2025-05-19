# Upgrade: Rails 5.1 to 5.2

## ✅ Checklist

- [ ] Update `rails` gem to `~> 5.2.0`
- [ ] Run `bundle update rails`
- [ ] Run `rails app:update` and resolve diffs
- [ ] Review ActiveStorage integration
- [ ] Replace legacy file attachments (if applicable)
- [ ] Review new credentials system vs secrets
- [ ] Update incompatible gems
- [ ] Run full test suite using Docker Compose

---

## 🧪 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
```

---

## 🔍 Known Changes

- ActiveStorage introduced
- Credentials management replaces secrets.yml
- Redis cache store support
- Content Security Policy (CSP) framework introduced

---

## 💥 Deprecation Warnings to Resolve

- Secrets.yml support deprecated
- Legacy file attachment methods

---

## 📚 Resources

- [FastRuby Upgrade Guide: 5.1 to 5.2](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-5-1-to-5-2.html)
- [Rails 5.2 Release Notes](https://guides.rubyonrails.org/5_2_release_notes.html)

---

## 🔁 Commands Run

```sh
bundle update rails
rails app:update
```

---

## 📦 Gems Reviewed

- `activestorage`
- `redis`
- `rspec-rails`
- `rails-controller-testing`

---

## 🧰 Issues & Fixes

- [ ] Review existing file uploads and migrate to ActiveStorage
- [ ] Enable `rails credentials:edit` and migrate secrets
- [ ] CSP headers to be added as needed
