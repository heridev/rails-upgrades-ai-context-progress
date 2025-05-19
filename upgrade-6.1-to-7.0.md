# Upgrade: Rails 6.1 to 7.0

## ✅ Checklist

- [ ] Replace Webpacker with `jsbundling-rails` or `importmap-rails`
- [ ] Install and configure Hotwire (Turbo + Stimulus)
- [ ] Replace synchronous query loading with `load_async`
- [ ] Remove deprecated synchronous loading patterns
- [ ] Remove legacy `before_action` usage
- [ ] Update all `params[:controller]` usages if controller nesting changes
- [ ] Run `rails app:update` and merge changes carefully
- [ ] Verify encrypted attribute usage if needed
- [ ] Review ActionText and ActiveStorage upgrades if used

---

## 🔪 Known Changes

- `webpacker` removed from default stack
- JS bundling defaults to `importmap-rails`, or use `jsbundling-rails` for esbuild/rollup
- CSS bundling uses `cssbundling-rails`
- Hotwire (Turbo + Stimulus) introduced by default
- Encrypted attributes support
- Synchronous query loading deprecated

---

## 💥 Deprecation Warnings to Resolve

- Remove deprecated `before_action` syntax if issues arise
- Remove old-style `params[:controller]` or controller nesting issues
- Replace synchronous query loading with `load_async`

---

## 📚 Resources

- [FastRuby Upgrade Guide: 6.1 to 7.0](https://www.fastruby.io/blog/rails/upgrades/rails-upgrade-guide-6-1-to-7-0.html)
- [Rails 7.0 Release Notes](https://guides.rubyonrails.org/7_0_release_notes.html)
- [Rails 7 Frontend Setup](https://github.com/rails/rails/blob/main/guides/source/javascript.md)

---

## ✏️ Commands Run

```sh
bundle update rails
rails app:update
```

---

## 📦 Gems Reviewed

- `importmap-rails` / `jsbundling-rails`
- `stimulus-rails`, `turbo-rails`
- `active_model_serializers`
- `rspec-rails`, `factory_bot_rails`

---

## 🪠 Issues & Fixes

- ❗ If Webpacker is still referenced in your app, remove it and replace with new JS/CSS bundling setup
- ✅ Migrated all uses of Webpacker to `jsbundling-rails` using esbuild
- 🛠️ ActionText attachments required change in storage references due to encrypted URLs
- 🧪 Added test coverage for any `load_async` usage to ensure correctness

---

## 🔹 Testing Instructions

```sh
docker compose exec web bundle install
docker compose run web rails db:migrate
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec
```
