# Upgrade: Rails 4.2 to 5.0

## ✅ Checklist

- [x] Update `rails` gem to `~> 5.0.0`
- [x] Run `bundle update rails`
- [x] Run `rails app:update` and review file diffs
- [x] Update `config/secrets.yml`
- [x] Replace `before_filter` with `before_action`
- [x] Replace deprecated test/unit code if used
- [x] Update strong parameters handling if necessary
- [x] Check for removed or renamed Rails components
- [x] Migrate from `rake` to `rails` CLI (e.g., `rake db:migrate` → `rails db:migrate`)
- [x] Update or replace incompatible gems
- [x] Run full test suite using Docker Compose

---

## 🧪 Testing Instructions

```sh
docker compose -f docker-compose.test.yml run --rm test_web bundle install
docker compose -f docker-compose.test.yml run --rm test_web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
```

---

## 🔍 Known Changes

- `ActionController::Parameters` is now required to be explicitly permitted
- `rake` CLI commands are now available through `rails`
- `ActiveRecord::Base.raise_in_transactional_callbacks` removed

---

## 💥 Deprecation Warnings to Resolve

- `before_filter` → `before_action`
- Params need explicit `permit` usage

---

## 📚 Resources

- [FastRuby Upgrade Guide: 4.2 to 5.0](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-4-2-to-5-0.html)
- [Rails 5.0 Release Notes](https://guides.rubyonrails.org/5_0_release_notes.html)

---

## 🔁 Commands Run

```sh
docker compose -f docker-compose.test.yml run --rm test_web bundle update rails
docker compose -f docker-compose.test.yml run --rm test_web rails app:update
```

---

## 📦 Gems Reviewed

- `devise`
- `paperclip` (deprecated — plan to migrate to ActiveStorage in Rails 5.2+)
- `will_paginate`
- `pg`, `sidekiq`, `rspec-rails`

---

## 🧰 Issues & Fixes

- [x] Needed to refactor `ActionController::Parameters` usage
- [x] `rspec-rails` version conflict — need to pin compatible version
