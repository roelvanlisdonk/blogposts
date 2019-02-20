---
ID: 3200
post_title: >
  Manually create the SQL Server tables
  used by de SimpleMembershipProvider
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/15/manually-create-the-sql-server-tables-used-by-de-simplemembershipprovider/
published: true
post_date: 2013-04-15 15:34:16
---
<p>&#160;</p>  <p>Below you will find the t-sql code needed to generate de SQL Server SimpleMembershipProvider tables.</p>  <p>&#160;</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">set ansi_nulls on
go
set quoted_identifier on
go

if </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.webpages_Membership'</span><span style="background: white; color: gray">) is null
</span><span style="background: white; color: blue">begin
    create table </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_Membership
    </span><span style="background: white; color: gray">(
        </span><span style="background: white; color: black">UserId                                    </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">not null </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">PK_Membership_UserId </span><span style="background: white; color: blue">primary key</span><span style="background: white; color: gray">,
        </span><span style="background: white; color: black">CreateDate                                </span><span style="background: white; color: blue">datetime </span><span style="background: white; color: gray">null,
        </span><span style="background: white; color: black">ConfirmationToken                        </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">128</span><span style="background: white; color: gray">) null,
        </span><span style="background: white; color: black">IsConfirmed                                </span><span style="background: white; color: blue">bit </span><span style="background: white; color: gray">null </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">DF_Membership_IsConfirmed </span><span style="background: white; color: blue">default </span><span style="background: white; color: gray">(</span><span style="background: white; color: black">0</span><span style="background: white; color: gray">),
        </span><span style="background: white; color: black">LastPasswordFailureDate                    </span><span style="background: white; color: blue">datetime </span><span style="background: white; color: gray">null,
        </span><span style="background: white; color: black">PasswordFailuresSinceLastSuccess        </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">not null </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">DF_Membership_PasswordFailuresSinceLastSuccess </span><span style="background: white; color: blue">default </span><span style="background: white; color: gray">(</span><span style="background: white; color: black">0</span><span style="background: white; color: gray">),
        </span><span style="background: white; color: black">[Password]                                </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">128</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: black">PasswordChangedDate                        </span><span style="background: white; color: blue">datetime </span><span style="background: white; color: gray">null,
        </span><span style="background: white; color: black">PasswordSalt                            </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">128</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: black">PasswordVerificationToken                </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">128</span><span style="background: white; color: gray">) null,
        </span><span style="background: white; color: black">PasswordVerificationTokenExpirationDate    </span><span style="background: white; color: blue">datetime </span><span style="background: white; color: gray">null
    )
</span><span style="background: white; color: blue">end
go
</span></pre>

<pre class="code"><span style="background: white; color: blue">set ansi_nulls on
go
set quoted_identifier on
go

if </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.webpages_Roles'</span><span style="background: white; color: gray">) is null
</span><span style="background: white; color: blue">begin
    create table </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_Roles
    </span><span style="background: white; color: gray">(
        </span><span style="background: white; color: black">RoleId </span><span style="background: white; color: blue">int identity</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">1</span><span style="background: white; color: gray">,</span><span style="background: white; color: black">1</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: black">RoleName </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">256</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">PK_Roles_RoleId </span><span style="background: white; color: blue">primary key clustered 
        </span><span style="background: white; color: gray">(
            </span><span style="background: white; color: black">RoleId </span><span style="background: white; color: blue">ASC
        </span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">pad_index </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">statistics_norecompute </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">ignore_dup_key </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_row_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_page_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">[PRIMARY]</span><span style="background: white; color: gray">,
        </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">UQ_Roles_RoleName </span><span style="background: white; color: blue">unique nonclustered 
        </span><span style="background: white; color: gray">(
            </span><span style="background: white; color: black">RoleName </span><span style="background: white; color: blue">asc
        </span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">pad_index </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">statistics_norecompute </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">ignore_dup_key </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_row_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_page_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">[PRIMARY]
    </span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">end
go
</span></pre>


<pre class="code"><span style="background: white; color: blue">set ansi_nulls on
go
set quoted_identifier on
go

if </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.webpages_OAuthMembership'</span><span style="background: white; color: gray">) is null
</span><span style="background: white; color: blue">begin
    create table </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_OAuthMembership
    </span><span style="background: white; color: gray">(
        </span><span style="background: white; color: black">Provider        </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">30</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: black">ProviderUserId    </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">100</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: black">UserId            </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">not null,
        </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">PK_OAuthMembership_Provider_ProviderUserId </span><span style="background: white; color: blue">primary key clustered 
        </span><span style="background: white; color: gray">(
            </span><span style="background: white; color: black">Provider </span><span style="background: white; color: blue">asc</span><span style="background: white; color: gray">,
            </span><span style="background: white; color: black">ProviderUserId </span><span style="background: white; color: blue">asc
        </span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">with    </span><span style="background: white; color: gray">(    </span><span style="background: white; color: blue">pad_index </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, 
                    </span><span style="background: white; color: blue">statistics_norecompute </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">,
                    </span><span style="background: white; color: blue">ignore_dup_key </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">,
                    </span><span style="background: white; color: blue">allow_row_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">,
                    </span><span style="background: white; color: blue">allow_page_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">[PRIMARY]
    </span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">end
go
</span></pre>


<pre class="code"><span style="background: white; color: blue">set ansi_nulls on
go
set quoted_identifier on
go

if </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.webpages_UserProfile'</span><span style="background: white; color: gray">) is null
</span><span style="background: white; color: blue">begin
    create table </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_UserProfile
    </span><span style="background: white; color: gray">(
        </span><span style="background: white; color: black">UserId </span><span style="background: white; color: blue">int identity</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">1</span><span style="background: white; color: gray">,</span><span style="background: white; color: black">1</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: black">UserName </span><span style="background: white; color: blue">nvarchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">56</span><span style="background: white; color: gray">) not null,
        </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">PK_UserProfile_UserId </span><span style="background: white; color: blue">primary key clustered 
        </span><span style="background: white; color: gray">(
            </span><span style="background: white; color: black">UserId </span><span style="background: white; color: blue">asc
        </span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">pad_index </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">statistics_norecompute </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">ignore_dup_key </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_row_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_page_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">[PRIMARY]</span><span style="background: white; color: gray">,
        </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">UQ_UserProfile_UserName </span><span style="background: white; color: blue">unique nonclustered 
        </span><span style="background: white; color: gray">(
            </span><span style="background: white; color: black">UserName </span><span style="background: white; color: blue">asc
        </span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">pad_index </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">statistics_norecompute </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">ignore_dup_key </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_row_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_page_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">[PRIMARY]
    </span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">end
go
</span></pre>


<pre class="code"><span style="background: white; color: blue">set ansi_nulls on
go
set quoted_identifier on
go

if </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.webpages_UsersInRoles'</span><span style="background: white; color: gray">) is null
</span><span style="background: white; color: blue">begin
    create table </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_UsersInRoles
    </span><span style="background: white; color: gray">(
        </span><span style="background: white; color: black">UserId </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">not null </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">FK_UsersInRoles_UserId </span><span style="background: white; color: blue">foreign key</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">UserId</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">references </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_UserProfile </span><span style="background: white; color: gray">(</span><span style="background: white; color: black">UserId</span><span style="background: white; color: gray">),
        </span><span style="background: white; color: black">RoleId </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">not null </span><span style="background: white; color: blue">constraint </span><span style="background: white; color: black">FK_UsersInRoles_RoleId </span><span style="background: white; color: blue">foreign key</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">RoleId</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">references </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">webpages_Roles </span><span style="background: white; color: gray">(</span><span style="background: white; color: black">RoleId</span><span style="background: white; color: gray">),
        </span><span style="background: white; color: blue">primary key clustered 
        </span><span style="background: white; color: gray">(
            </span><span style="background: white; color: black">UserId </span><span style="background: white; color: blue">asc</span><span style="background: white; color: gray">,
            </span><span style="background: white; color: black">RoleId </span><span style="background: white; color: blue">asc
        </span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">pad_index </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">statistics_norecompute </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">ignore_dup_key </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">off</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_row_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">, </span><span style="background: white; color: blue">allow_page_locks </span><span style="background: white; color: gray">= </span><span style="background: white; color: blue">on</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on PRIMARY</span><span style="background: white; color: black">]
    </span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">end
go
</span></pre>