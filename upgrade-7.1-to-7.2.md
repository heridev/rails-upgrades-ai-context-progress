# Upgrade: Rails 7.1 to 7.2

## ✅ Checklist

- [ ] Update `rails` and related gems
- [ ] Run `rails app:update` and merge config changes
- [ ] Address any new deprecation warnings
- [ ] Validate Zeitwerk autoload paths
- [ ] Validate ActionCable and ActionMailer configurations
- [ ] Review test suite and refactor if needed

---

## 🔪 Known Changes

- `zeitwerk` autoloader improvements, especially in engines
- `ActionCable`: Improved broadcasting and connection lifecycle hooks
- Enhanced `ActiveJob` instrumentation and logging
- New default `config.add_autoload_paths_to_load_path = false`
- Reorganized generators and configuration defaults

---

## 💥 Deprecation Warnings to Resolve

- Ensure all `lib/` code is eager-load safe or move to `app/`
- `ActiveRecord::Base.raise_in_transactional_callbacks` is removed
- Deprecated callbacks API (use `after_commit` style only)

---

## 📚 Resources

- [Rails 7.2 Release Notes](https://guides.rubyonrails.org/7_2_release_notes.html)
- [FastRuby Upgrade Guide: 7.1 to 7.2](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-7-1-to-7-2.html)
- [Zeitwerk for Rails](https://github.com/fxn/zeitwerk)

---

## ✏️ Commands Run

```sh
bundle update rails
rails app:update
```

---

## 🛆 Gems Reviewed

- `rspec-rails`, `factory_bot_rails`
- `stimulus-rails`, `turbo-rails`
- Any internal engines using `Zeitwerk`

---

## 🪠 Issues & Fixes

- Fixed failing tests due to changed eager loading behavior
- Migrated deprecated callbacks to supported hooks

---

## 🔹 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
```
