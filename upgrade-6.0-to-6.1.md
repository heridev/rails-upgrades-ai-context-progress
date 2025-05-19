# Upgrade: Rails 6.0 to 6.1

## ✅ Checklist

- [ ] Update `rails` gem to `~> 6.1.0`
- [ ] Run `bundle update rails`
- [ ] Run `rails app:update` and apply diff cautiously
- [ ] Switch to Zeitwerk autoloader (default in 6.1)
- [ ] Update credentials format (if not yet done)
- [ ] Use new error objects from `ActiveModel::Errors`
- [ ] Enable new per-database connection switching (if using multiple DBs)
- [ ] Revisit any monkey patches or initializers for compatibility
- [ ] Full regression test suite in Docker Compose

---

## 🧪 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
```

---

## 🔍 Known Changes

- Zeitwerk is now default and mandatory
- Improved support for multi-DB applications
- New `ActiveModel::Errors` API (breaking for some)
- Encrypted credentials improvement (per-environment supported)

---

## 💥 Deprecation Warnings to Resolve

- Use of classic autoloader removed
- `ActiveModel::Errors#[]` no longer returns an array
- Deprecated `rails test` flags

---

## 📚 Resources

- [FastRuby Upgrade Guide: 6.0 to 6.1](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-6-0-to-6-1.html)
- [Rails 6.1 Release Notes](https://guides.rubyonrails.org/6_1_release_notes.html)

---

## 🔁 Commands Run

```sh
bundle update rails
rails app:update
```

---

## 📦 Gems Reviewed

- `zeitwerk`
- `rspec-rails`
- `factory_bot_rails`
- `active_model_serializers`
- `webmock`

---

## 🧰 Issues & Fixes

- [ ] Ensure app boots with Zeitwerk (class naming, file paths)
- [ ] Fix `ActiveModel::Errors` test failures
- [ ] Update credential access methods in initializers/configs
- [ ] Add database role switching if needed for replicas
