# Upgrade: Rails 5.0 to 5.1

## ✅ Checklist

- [ ] Update `rails` gem to `~> 5.1.0`
- [ ] Run `docker compose -f docker-compose.test.yml run --rm test_web bundle update rails`
- [ ] Run `docker compose -f docker-compose.test.yml run --rm test_web rails app:update` and review file diffs
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
docker compose -f docker-compose.test.yml run --rm test_web bundle install
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/controllers/api/v1/patients_controller_spec.rb
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/features/patients/managing_patient_histories_spec.rb
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
docker compose -f docker-compose.test.yml run --rm test_web bundle update rails
docker compose -f docker-compose.test.yml run --rm test_web rails app:update
docker compose -f docker-compose.test.yml run --rm test_web EDITOR=vi rails credentials:edit
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

- [ ] Migrated integration tests to system specs where applicable
- [ ] Verified all forms use `form_with` helper
- [ ] Secrets moved to encrypted credentials
- [ ] Yarn installation and Webpacker integration tested inside Docker
- [ ] Removed or replaced `rails-controller-testing` where required
