# Upgrade: Rails 5.0 to 5.1

## ✅ Checklist

- [ ] Update `rails` gem to `~> 5.1.0`
- [ ] Run `bundle update rails`
- [ ] Run `rails app:update` and review file diffs
- [ ] Enable encrypted secrets (optional)
- [ ] Verify compatibility of `form_with`
- [ ] Switch from `form_for`/`form_tag` to `form_with` if desired
- [ ] Replace `rails-controller-testing` if deprecated
- [ ] Migrate tests to system specs if using Capybara
- [ ] Update or replace incompatible gems
- [ ] Run full test suite using Docker Compose

---

## 🧪 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/controllers/api/v1/patients_controller_spec.rb:319
```

---

## 🔍 Known Changes

- `form_with` introduced (replaces `form_for`, `form_tag`)
- System tests added with Capybara support
- Yarn introduced for JavaScript package management
- Encrypted secrets support added via `config/secrets.yml.enc`
- JavaScript now handled through Webpacker (optional)
- Default Rails scaffold uses system tests with Capybara

---

## 💥 Deprecation Warnings to Resolve

- `form_for` and `form_tag` not deprecated, but no longer recommended
- Integration tests considered legacy; prefer system specs
- `rails-controller-testing` might not be actively maintained

---

## 📚 Resources

- [FastRuby Upgrade Guide: 5.0 to 5.1](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-5-0-to-5-1.html)
- [Rails 5.1 Release Notes](https://guides.rubyonrails.org/5_1_release_notes.html)

---

## 🔁 Commands Run

```sh
bundle update rails
rails app:update
EDITOR=nano rails credentials:edit
```

---

## 📦 Gems Reviewed

- `webpacker`: Consider adding for modern JS support
- `rails-controller-testing`: Replace with controller specs in `rspec-rails` or system tests
- `capybara`: Update to latest stable version
- `rspec-rails`: Ensure compatibility with 5.1 and system specs
- `yarn`: Confirm installed and configured within Docker environment

---

## 🧰 Issues & Fixes

- [x] Migrated integration tests to system specs where applicable
- [x] Verified all forms use `form_with` helper
- [x] Secrets moved to encrypted credentials
- [x] Yarn installation and Webpacker integration tested inside Docker
- [x] Removed or replaced `rails-controller-testing` where required
