# Upgrade: Rails 4.2 to 5.0

## ✅ Checklist

- [ ] Update `rails` gem to `~> 5.0.0`
- [ ] Run `bundle update rails`
- [ ] Run `rails app:update` and review file diffs
- [ ] Update `config/secrets.yml`
- [ ] Replace `before_filter` with `before_action`
- [ ] Replace deprecated test/unit code if used
- [ ] Update strong parameters handling if necessary
- [ ] Check for removed or renamed Rails components
- [ ] Migrate from `rake` to `rails` CLI (e.g., `rake db:migrate` → `rails db:migrate`)
- [ ] Update or replace incompatible gems
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
bundle update rails
rails app:update
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
- [ ] `rspec-rails` version conflict — need to pin compatible version
