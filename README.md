Multi-Threaded/Multi-Node Utilities (Mutil)
===========================================

Copies between local file systems are a daily activity.  Files are
constantly being moved to locations accessible by systems with different
functions and/or storage limits, being backed up and restored, or being
moved due to upgraded and/or replaced hardware.  Hence, maximizing the
performance of copies as well as checksums that ensure the integrity of
copies is desirable to minimize the turnaround time of user and
administrator activities.  Modern parallel file systems provide very
high performance for such operations using a variety of techniques such
as striping files across multiple disks to increase aggregate I/O
bandwidth and spreading disks across multiple servers to increase
aggregate interconnect bandwidth.

To achieve peak performance from such systems, it is typically
necessary to utilize multiple concurrent readers/writers from multiple
systems to overcome various single-system limitations such as number of
processors and network bandwidth.  The standard cp and md5sum tools of
GNU coreutils found on every modern Unix/Linux system, however, utilize
a single execution thread on a single CPU core of a single system, hence
cannot take full advantage of the increased performance of clustered
file systems.

Mutil provides mcp and msum, which are drop-in replacements for cp and
md5sum that utilize multiple types of parallelism to achieve maximum
copy and checksum performance on clustered file systems.
Multi-threading is used to ensure that nodes are kept as busy as
possible.  Read/write parallelism allows individual operations of a
single copy to be overlapped using asynchronous I/O.  Multi-node
cooperation allows different nodes to take part in the same
copy/checksum.  Split file processing allows multiple threads to
operate concurrently on the same file.  Finally, hash trees allow
inherently serial checksums to be performed in parallel.

For full details of the mcp and msum implementations and their (old)
expected performance, see https://pkolano.github.io/papers/lisa10.pdf.
For installation details, see "INSTALL".  For usage details, see
"doc/usage.txt".

Questions, comments, fixes, and/or enhancements welcome.

--Paul Kolano <paul.kolano@nasa.gov>

