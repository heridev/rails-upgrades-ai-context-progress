# Upgrade: Rails 7.0 to 7.1

## ✅ Checklist

- [ ] Update `rails` and related dependencies in Gemfile
- [ ] Run `rails app:update` and review all file changes
- [ ] Replace `after_initialize` hooks with initializers
- [ ] Ensure `ActionMailer` background jobs use properly configured queue adapters
- [ ] Verify `Zeitwerk` eager loading behavior for engines
- [ ] Set `config.load_defaults 7.1` and adjust configs accordingly
- [ ] Run full test suite to catch deprecations or behavior changes

---

## 🔪 Known Changes

- Zeitwerk eager loading by default for engines
- Config changes in `config/application.rb` (e.g. `config.enable_reloading = true`)
- ActionMailer `deliver_later` may now raise if ActiveJob is misconfigured
- `Rails::Application::Configuration#after_initialize` is deprecated, use initializers
- `config.load_defaults 7.1` enables new behaviors, including `ActionController::Base.allow_forgery_protection = true` by default in all environments

---

## 💥 Deprecation Warnings to Resolve

- Replace `after_initialize` hooks with dedicated initializers
- Review all `deliver_later` usage and ensure queue adapters are correctly configured
- Test eager loading for engines or internal gems with Zeitwerk

---

## 📚 Resources

- [Rails 7.1 Release Notes](https://guides.rubyonrails.org/7_1_release_notes.html)
- [Zeitwerk Updates in 7.1](https://github.com/fxn/zeitwerk#rails-engines)
- [Upgrade Guide 7.0 to 7.1](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-7-0-to-7-1.html)

---

## ✏️ Commands Run

```sh
bundle update rails
rails app:update
```

---

## 📦 Gems Reviewed

- `active_model_serializers`
- `rspec-rails`, `factory_bot_rails`
- Custom internal engines

---

## 🪠 Issues & Fixes

- `deliver_later` calls were failing due to missing queue adapters — added `config.active_job.queue_adapter = :sidekiq`
- Refactored `after_initialize` code blocks into proper initializers in `config/initializers/`
- Fixed eager loading issues by explicitly requiring modules inside internal engines

---

## 🔹 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
```
