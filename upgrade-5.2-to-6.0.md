# Upgrade: Rails 5.2 to 6.0

## ✅ Checklist

- [ ] Update `rails` gem to `~> 6.0.0`
- [ ] Run `docker compose -f docker-compose.test.yml run --rm test_web bundle update rails`
- [ ] Run `docker compose -f docker-compose.test.yml run --rm test_web rails app:update` and resolve configuration diffs
- [ ] Review Zeitwerk autoloader changes (optional in 6.0, default in 6.1)
- [ ] Check Action Mailbox and Action Text (optional new frameworks)
- [ ] Handle deprecations and upgrade paths
- [ ] Test thoroughly with Docker Compose

---

## 🧪 Testing Instructions

```sh
docker compose -f docker-compose.test.yml run --rm test_web bundle install
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/controllers/api/v1/patients_controller_spec.rb
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/features/patients/managing_patient_histories_spec.rb
```

---

## 🔍 Known Changes

- Action Mailbox and Action Text introduced
- Multiple database support (basic version)
- Zeitwerk autoloader added (not default yet)
- Parallel testing support added
- Credentials structure updated

---

## 💥 Deprecation Warnings to Resolve

- Classic autoloader is deprecated (Zeitwerk preferred in future)
- Legacy test file structure may need updating
- Secrets in `config/secrets.yml` should be removed

---

## 📚 Resources

- [FastRuby Upgrade Guide: 5.2 to 6.0](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-5-2-to-6-0.html)
- [Rails 6.0 Release Notes](https://guides.rubyonrails.org/6_0_release_notes.html)

---

## 🔁 Commands Run

```sh
docker compose -f docker-compose.test.yml run --rm test_web bundle update rails
docker compose -f docker-compose.test.yml run --rm test_web rails app:update
```

---

## 📦 Gems Reviewed

- `zeitwerk`
- `actiontext`
- `actionmailbox`
- `redis`
- `rspec-rails`
- `webmock`

---

## 🧰 Issues & Fixes

- [ ] Ensure autoload paths are compatible with Zeitwerk
- [ ] Resolve `Zeitwerk::NameError` issues on boot
- [ ] Configure `storage.yml` for ActionText if used
- [ ] Run tests in parallel to verify support
