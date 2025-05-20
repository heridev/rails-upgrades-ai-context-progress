# Upgrade: Rails 5.1 to 5.2

## ✅ Checklist

- [ ] Update `rails` gem to `~> 5.2.0`
- [ ] Run `docker compose -f docker-compose.test.yml run --rm test_web bundle update rails`
- [ ] Run `docker compose -f docker-compose.test.yml run --rm test_web rails app:update` and resolve diffs
- [ ] Review ActiveStorage integration
- [ ] Replace legacy file attachments (if applicable)
- [ ] Review new credentials system vs secrets
- [ ] Update incompatible gems
- [ ] Run full test suite using Docker Compose
- [ ] Upgrade to ruby 3 so at this point we can make the `active-import` gem to work in Ruby 3

```
ArgumentError: wrong number of arguments (given 3, expected 2)
in activerecord-import-0.17.2 with Rails 5.0.7.2 and Ruby 3.0.
What we know:
Gemfile and Gemfile.lock both specify activerecord-import 0.17.2.
This version is supposed to be compatible with Rails 5.0.x, but not with Ruby 3.0.
The error is a known incompatibility: activerecord-import 0.17.2 does not support Ruby 3.0, only up to Ruby 2.7.
Solution:
You must downgrade Ruby to 2.7.x (e.g., 2.7.7) for this step of the upgrade.
Rails 5.0.x + activerecord-import 0.17.x is only supported on Ruby 2.7 or lower.
Ruby 3.0 support for activerecord-import starts with Rails 5.2+ and activerecord-import 1.0+.
```

---

## 🧪 Testing Instructions

```sh
docker compose -f docker-compose.test.yml run --rm test_web bundle install
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/controllers/api/v1/patients_controller_spec.rb
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/features/patients/managing_patient_histories_spec.rb
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
docker compose -f docker-compose.test.yml run --rm test_web bundle update rails
docker compose -f docker-compose.test.yml run --rm test_web rails app:update
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
- [ ] Enable `docker compose -f docker-compose.test.yml run --rm test_web rails credentials:edit` and migrate secrets
- [ ] CSP headers to be added as needed
