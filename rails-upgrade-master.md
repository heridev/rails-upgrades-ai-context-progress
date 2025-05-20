# Rails Upgrade Master Plan

This document tracks the upgrade of our Rails application from **Rails 4.2 to Rails 7.2**. Each version upgrade has its own markdown file. Use this checklist and notes section to track progress and record global upgrade details.

## 📦 Gem Compatibility and Analysis

Upgrading Rails requires careful auditing of your application’s gems to ensure they work well with the new Rails version. This section outlines explicit steps and files to check.

### Files to Review

- `Gemfile` — lists all gems your app depends on (with version constraints)
- `Gemfile.lock` — records the exact gem versions currently installed
- `Dockerfile` — make sure the right ruby version matches the right upgrade and gems

### Step-by-Step Gem Analysis and Upgrade Process

1. **Extract the list of gems and their versions** from `Gemfile` and `Gemfile.lock`.

   - You can programmatically parse these files to get gem names and versions.

2. **Check gem compatibility:**

   - Visit the gem’s official repository (e.g., GitHub) and review their changelog, issues, or README for Rails version compatibility notes.
   - Look for any open issues or pull requests related to the target Rails version.

3. **Identify outdated gems:**

   - Run locally or in your Docker container:
     ```bash
     docker compose -f docker-compose.test.yml run --rm test_web bundle outdated
     ```
   - This command lists gems with newer versions available, including if updates fix Rails compatibility.

4. **Update gems that are compatible with the target Rails version:**

   - For a specific gem:
     ```bash
     docker compose -f docker-compose.test.yml run --rm test_web bundle update gem_name
     ```
   - Or update all gems at once (be cautious):
     ```bash
     docker compose -f docker-compose.test.yml run --rm test_web bundle update
     ```
   - After updating, run:
     ```bash
     docker compose -f docker-compose.test.yml run --rm test_web bundle install
     ```
   - This ensures your Docker environment uses the updated gems.

5. **Remove or replace gems:**

   - If a gem is no longer maintained or incompatible, consider removing it or finding an alternative.
   - Update your `Gemfile` accordingly and run `docker compose -f docker-compose.test.yml run --rm test_web bundle install`.

6. **Test your app extensively:**

   - Run your full test suite to catch issues caused by gem upgrades.
   - Pay attention to deprecation warnings or runtime errors related to gems.

7. **Document your gem changes:**
   - Keep a record of updated gems, removed gems, and any configuration changes needed, can you create a file and keep it updated whenever there is an update it could be a file called `updated_removed_gems.txt`
   - Note any issues encountered and how they were resolved in the same file with a sort of history and datetime.

### Tools and Tips

- Use `docker compose -f docker-compose.test.yml run --rm test_web bundle outdated` to get a quick report on gems that can be updated.
- Check [RubyGems.org](https://rubygems.org/) or GitHub repos for latest gem versions and release notes.

---

📁 Directory Structure

```bash
rails-upgrade/
│
├── rails-upgrade-master.md
├── upgrade-4.2-to-5.0.md
├── upgrade-5.0-to-5.1.md
├── upgrade-5.1-to-5.2.md
├── upgrade-5.2-to-6.0.md
├── upgrade-6.0-to-6.1.md
├── upgrade-6.1-to-7.0.md
├── upgrade-7.0-to-7.1.md
└── upgrade-7.1-to-7.2.md
```

---

## ✅ Progress Checklist

- [x] [4.2 to 5.0](./upgrade-4.2-to-5.0.md)
- [ ] [5.0 to 5.1](./upgrade-5.0-to-5.1.md)
- [ ] [5.1 to 5.2](./upgrade-5.1-to-5.2.md)
- [ ] [5.2 to 6.0](./upgrade-5.2-to-6.0.md)
- [ ] [6.0 to 6.1](./upgrade-6.0-to-6.1.md)
- [ ] [6.1 to 7.0](./upgrade-6.1-to-7.0.md)
- [ ] [7.0 to 7.1](./upgrade-7.0-to-7.1.md)
- [ ] [7.1 to 7.2](./upgrade-7.1-to-7.2.md)

---

## 🛠️ Docker Compose Usage after a important upgrade

All tests and development tasks are run using Docker Compose:

```sh
docker compose -f docker-compose.test.yml run --rm test_web bundle install
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/controllers/api/v1/patients_controller_spec.rb
docker compose -f docker-compose.test.yml run --rm test_web bundle exec rspec ./spec/features/patients/managing_patient_histories_spec.rb
```

---

## 💡 Global Upgrade Notes

- Always run a few of the rspec tests above after applying changes
- Use `docker compose -f docker-compose.test.yml run --rm test_web rails app:update` and review diffs carefully
- Pay attention to deprecation warnings
- Upgrade third-party gems gradually with each Rails version
- Lock major versions of gems until you fully test compatibility
- Consider using `bundler-audit`, `brakeman`, and `rubocop` for code health

---

## Whenever there is a chance to upgrade the Ruby version and build is working:

Make sure all the following are true before moving on to the next step

- [ ] All gems are working as expected and they are all compatible between each other
- [ ] Generate the new Gemfile.lock using docker compose and docker-compose -f docker-compose.test.yml run --rm test_web bundle install

Continue with each version-specific markdown file for detailed steps and version notes.
