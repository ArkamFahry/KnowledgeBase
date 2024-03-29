# Cron Job
	- In general terms, a Cron job is a scheduled task or job that runs automatically at specified intervals on a Unix-like operating system. The name "Cron" comes from the Greek word "[Chronos](https://en.wikipedia.org/wiki/Chronos)" meaning time, and it's commonly used for automating repetitive tasks, such as system maintenance, backups, or other periodic processes.
	- Working of Cron jobs
		- **Cron Daemon**
			- The Cron job is managed by a daemon (a background process) called "Cron." The Cron daemon constantly checks a configuration file, typically known as the "crontab" (short for Cron table), for scheduled tasks.
		- **Crontab**
			- The crontab is a file that contains a list of commands and the timing information for when those commands should be executed. Each line in the crontab represents a separate job, and it includes details such as the minute, hour, day of the month, month, and day of the week when the job should run.
		- **Syntax**
			- The syntax for specifying the schedule in a crontab entry involves five fields representing different time units
				- Minute (0-59)
				- Hour (0-23)
				- Day of the month (1-31)
				- Month (1-12 or names like "Jan," "Feb," etc.)
				- Day of the week (0-6 or names like "Sun," "Mon," etc.)
				- For example, a crontab entry like `0 2 * * *` means the job will run at 2:00 AM every day.
		- **Automated Execution**
			- The Cron daemon checks the crontab at regular intervals, and when it finds a job whose schedule matches the current time, it executes the specified command.
	- Cron jobs are versatile and widely used for automating various system and application-related tasks, making them an essential part of system administration and automation on Unix-like systems. They provide a convenient way to schedule repetitive tasks without manual intervention.