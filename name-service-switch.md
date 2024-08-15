# Name Service Switch

## files-pwd.c

> glibc/nss/nss_files/files-pwd.c

```c
/* User file parser in nss_files module.
 * ...
 */
...
/* Our parser function is already defined in fgetpwent_r.c, so use that
   to parse lines from the database file.  */
...
#include "files-parse.c"
#include GENERIC

DB_LOOKUP (pwnam, '.', 0, ("%s", name),
	   {
	     if (name[0] != '+' && name[0] != '-'
		 && ! strcmp (name, result->pw_name))
	       break;
	   }, const char *name)

DB_LOOKUP (pwuid, '=', 20, ("%lu", (unsigned long int) uid),
	   {
	     if (result->pw_uid == uid && result->pw_name[0] != '+'
		 && result->pw_name[0] != '-')
	       break;
	   }, uid_t uid)
```

## files-parse

> glibc/nss/nss_files/files-parse.c

```c
/* Common code for file-based database parsers in nss_files module.
 * ...
 */
...
#ifndef GENERIC
# define GENERIC "files-XXX.c"
#endif
```

## files-XXX

> glibc/nss/nss_files/files-XXX.c

```c
/* Common code for file-based databases in nss_files module.
 * ...
 */
...
/* Parsing the database file into `struct STRUCTURE' data structures.  */
static enum nss_status
internal_getent (FILE *stream, struct STRUCTURE *result,
		 char *buffer, size_t buflen, int *errnop H_ERRNO_PROTO
		 EXTRA_ARGS_DECL)
{
  ...
  while (true)
    {
      ...
      /* Ignore empty and comment lines.  */
      if (*p == '\0' || *p == '#')
	continue;
      ...
    }
}
...
#define DB_LOOKUP(name, db_char, keysize, keypattern, break_if_match, proto...)\
enum nss_status								      \
_nss_files_get##name##_r (proto,					      \
			  struct STRUCTURE *result, char *buffer,	      \
			  size_t buflen, int *errnop H_ERRNO_PROTO)	      \
{									      \
  ...
  if (status == NSS_STATUS_SUCCESS)					      \
    {									      \
      while ((status = internal_getent (stream, result, buffer, buflen, errnop \
					H_ERRNO_ARG EXTRA_ARGS_VALUE))	      \
	     == NSS_STATUS_SUCCESS)					      \
	{ break_if_match }						      \
      ...								      \
    }									      \
  ...    								      \
}									      \
```
