# Upgrade: Rails 5.2 to 6.0

## ✅ Checklist

- [ ] Update `rails` gem to `~> 6.0.0`
- [ ] Run `bundle update rails`
- [ ] Run `rails app:update` and resolve configuration diffs
- [ ] Review Zeitwerk autoloader changes (optional in 6.0, default in 6.1)
- [ ] Check Action Mailbox and Action Text (optional new frameworks)
- [ ] Handle deprecations and upgrade paths
- [ ] Test thoroughly with Docker Compose

---

## 🧪 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
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
bundle update rails
rails app:update
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
