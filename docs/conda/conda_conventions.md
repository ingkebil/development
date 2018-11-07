# Conda conventions

- Avoid installing anything in the conda default environment (root) if possible
- Naming conventions for conda environments: 
   - Production: `[env_type=P]_[logical_name]_[creation_date]`
   - Development: `[env_type=D]_[logical_name]_[creation_date]_[signature]`
   - Archive: `[env_type=A]_[logical_name]_[timestamp]_[signature]`
      - env_type: environment types are
        - **D** (Develop),
        - **P** (Production),
        - or **A** (Archive).
      - creation_date: `%y%m%d`
      - timestamp: `%y%m%d %H%M%S`.
      - logical_name: whatever makes sense.
      - signature: something to show who created the environment. Use the two- or three letter name acronyms assigned to you.
