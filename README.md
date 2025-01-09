```python
import datetime
import random
import subprocess

def maak_commits(start_datum, eind_datum):
  """Maakt een Git repository aan en voegt commits toe op werkdagen 
  tussen 7 en 18 uur binnen de gegeven periode.

  Args:
    start_datum: datetime.date object voor de startdatum.
    eind_datum: datetime.date object voor de einddatum.
  """

  subprocess.run(["git", "init"])
  huidige_datum = start_datum

  while huidige_datum <= eind_datum:
    if huidige_datum.weekday() < 5:  # Maandag tot vrijdag
      for uur in range(7, 18):
        aantal_commits = random.randint(0, 5)  # Willekeurig aantal commits (0 tot 5)
        for _ in range(aantal_commits):
          # Maak een lege commit met een tijdstempel
          tijdstempel = huidige_datum.strftime("%Y-%m-%d") + "T" + str(uur).zfill(2) + ":00:00"
          subprocess.run(["git", "commit", "--allow-empty", "-m", "Commit", "--date", tijdstempel])
    huidige_datum += datetime.timedelta(days=1)

if __name__ == "__main__":
  start_datum = datetime.date(2024, 1, 1)
  eind_datum = datetime.date(2024, 12, 31)
  maak_commits(start_datum, eind_datum)
