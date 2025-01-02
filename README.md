# WordPress EC2 Deployment with Ansible

This project provides an automated solution for deploying a WordPress site on an AWS EC2 instance using Ansible. It includes additional features like MySQL setup with automatic backups and Prometheus/Grafana monitoring accessible via sub-URI.

## Features ✨

1. **EC2 Role** 🖥️
   - Launches an EC2 instance of type `t3.small` with Ubuntu 22.04.
   - Supports tasks to stop, start, and delete the EC2 instance.

2. **WordPress Role** 🌐
   - Installs Apache, PHP, and WordPress.
   - Configures WordPress for immediate use.

3. **MySQL Role** 🗄️
   - Installs MySQL 8.
   - Sets up a daily database backup cron job.

4. **Prometheus & Grafana Role** 📊
   - Installs Prometheus and Grafana on the same EC2 instance.
   - Configures Grafana to be accessible via `/grafana` sub-URI.

## Project Structure 📂

- `wordpress.yml` - Main playbook to execute all roles.
- Roles:
  - `ec2_instance`: Manages EC2 lifecycle.
  - `wordpress`: Installs and configures WordPress.
  - `mysql`: Installs MySQL and sets up backups.
  - `grafana_prometheus`: Deploys Prometheus and Grafana with reverse proxy setup.

## Usage 🚀

### Prerequisites:
- Ansible installed.
- AWS credentials configured.
- Necessary variables set in Ansible inventory or as extra variables (e.g., `aws_key_name`, `aws_region`, `ubuntu_22_04_ami`).

### Steps:
1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Run the playbook:
   ```bash
   ansible-playbook wordpress.yml
   ```

3. Access your deployed services:
   - WordPress: `http://<ec2-public-ip>`
   - Grafana: `http://<ec2-public-ip>/grafana`

## Notes 📝

- The `ec2_instance` and `mysql` roles are independent. You can use them in isolation for other projects.
- Use the following tags to manage EC2 states:
  - `stop`: Stop the EC2 instance.
  - `start`: Start the EC2 instance.
  - `delete`: Terminate the EC2 instance.

## Acceptance Tests ✅

1. Running the playbook `wordpress.yml` creates a ready-to-use WordPress instance. The public IP is displayed as a URL in the terminal.
2. The `ec2_instance` and `mysql` roles work independently on compatible systems.
3. EC2 instance lifecycle management (stop/start/delete) works via tasks or tags.

## Extra 🎁

- Prometheus and Grafana are installed on the same EC2 instance as WordPress.
- Grafana is accessible via the `/grafana` sub-URI without affecting the WordPress root path.

## Future Enhancements 🔮
- Add TLS support for WordPress and Grafana.
- Automate scaling for high traffic scenarios.

Enjoy deploying your WordPress with ease! 🌟

