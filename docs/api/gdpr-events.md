# GDPR Events

Framework Helper for GDPR (General Data Protection Regulation) compliance events.

---

## PersonalDataAccessed

Creates a personal data access event for GDPR Article 5(1)(f) compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent PersonalDataAccessed(
        string dataSubjectId,
        string actorUserId,
        string? dataCategory = null,
        string? lawfulBasis = null,
        string? purpose = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject whose personal data was accessed |
    | `actorUserId` | `string` | Yes | ID of user accessing the personal data |
    | `dataCategory` | `string?` | No | Category of personal data (e.g., "contact_information", "health_data") |
    | `lawfulBasis` | `string?` | No | Lawful basis for processing (e.g., "consent", "contract", "legal_obligation") |
    | `purpose` | `string?` | No | Purpose of access (e.g., "customer_support", "marketing") |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "data_processor", "admin") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant personal data access event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article5.personal_data.accessed`
    - **GDPR Article:** Article 5(1)(f) - Integrity and confidentiality
    - **Data Category:** Stored in framework data
    - **Lawful Basis:** Stored in framework data
    - **Purpose:** Stored in framework data
    - **Risk Level:** Low

=== "Example"

    **Example usage:**

    ```csharp
    var accessEvent = GdprEvents.PersonalDataAccessed(
        dataSubjectId: "user-123",
        actorUserId: "support-456",
        dataCategory: "contact_information",
        lawfulBasis: "consent",
        purpose: "customer_support",
        sessionId: "session789",
        ipAddress: "192.168.1.1",
        actorRole: "customer_support_agent"
    );

    await _auditLedger.LogEventAsync(accessEvent);
    ```

---

## PersonalDataProcessed

Creates a personal data processing event for GDPR Article 6 compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent PersonalDataProcessed(
        string dataSubjectId,
        string actorUserId,
        string processingActivity,
        string lawfulBasis,
        string? dataCategory = null,
        string? purpose = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject |
    | `actorUserId` | `string` | Yes | ID of user performing the processing |
    | `processingActivity` | `string` | Yes | Type of processing activity (e.g., "collection", "storage", "analysis") |
    | `lawfulBasis` | `string` | Yes | Lawful basis for processing (Article 6: consent, contract, legal_obligation, vital_interests, public_task, legitimate_interests) |
    | `dataCategory` | `string?` | No | Category of personal data being processed |
    | `purpose` | `string?` | No | Purpose of processing |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant personal data processing event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article6.personal_data.processed`
    - **GDPR Article:** Article 6 - Lawfulness of processing
    - **Processing Activity:** Stored in framework data
    - **Lawful Basis:** Stored in framework data (required)
    - **Risk Level:** Low

=== "Example"

    **Example usage:**

    ```csharp
    var processEvent = GdprEvents.PersonalDataProcessed(
        dataSubjectId: "user-123",
        actorUserId: "system",
        processingActivity: "collection",
        lawfulBasis: "consent",
        dataCategory: "contact_information",
        purpose: "account_registration",
        actorRole: "system"
    );

    await _auditLedger.LogEventAsync(processEvent);
    ```

---

## ConsentGiven

Creates a consent given event for GDPR Article 7 compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent ConsentGiven(
        string dataSubjectId,
        string consentType,
        string? purpose = null,
        string? consentMethod = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorUserId = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject giving consent |
    | `consentType` | `string` | Yes | Type of consent (e.g., "marketing", "analytics", "cookies") |
    | `purpose` | `string?` | No | Purpose for which consent is given |
    | `consentMethod` | `string?` | No | Method of consent (e.g., "checkbox", "button_click", "explicit") |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of data subject |
    | `actorUserId` | `string?` | No | ID of user (if consent given on behalf of data subject) |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant consent given event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article7.consent.given`
    - **GDPR Article:** Article 7 - Conditions for consent
    - **Consent Type:** Stored in framework data
    - **Consent Method:** Stored in framework data
    - **Risk Level:** Low

=== "Example"

    **Example usage:**

    ```csharp
    var consentEvent = GdprEvents.ConsentGiven(
        dataSubjectId: "user-123",
        consentType: "marketing",
        purpose: "email_campaigns",
        consentMethod: "checkbox",
        sessionId: "session456",
        ipAddress: "192.168.1.1"
    );

    await _auditLedger.LogEventAsync(consentEvent);
    ```

---

## ConsentWithdrawn

Creates a consent withdrawal event for GDPR Article 7(3) compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent ConsentWithdrawn(
        string dataSubjectId,
        string consentType,
        string? reason = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorUserId = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject withdrawing consent |
    | `consentType` | `string` | Yes | Type of consent being withdrawn |
    | `reason` | `string?` | No | Reason for withdrawal (optional) |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of data subject |
    | `actorUserId` | `string?` | No | ID of user (if withdrawal processed by staff) |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant consent withdrawal event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article7.consent.withdrawn`
    - **GDPR Article:** Article 7(3) - Right to withdraw consent
    - **Consent Type:** Stored in framework data
    - **Withdrawal Reason:** Stored in framework data
    - **Risk Level:** Medium

=== "Example"

    **Example usage:**

    ```csharp
    var withdrawEvent = GdprEvents.ConsentWithdrawn(
        dataSubjectId: "user-123",
        consentType: "marketing",
        reason: "user_preference",
        sessionId: "session456",
        ipAddress: "192.168.1.1"
    );

    await _auditLedger.LogEventAsync(withdrawEvent);
    ```

---

## DataSubjectRequest

Creates a data subject rights request event for GDPR Articles 15-22 compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent DataSubjectRequest(
        string dataSubjectId,
        string requestType,
        string actorUserId,
        string? requestDetails = null,
        string? status = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject making the request |
    | `requestType` | `string` | Yes | Type of request (e.g., "access", "rectification", "erasure", "portability", "restriction", "objection") |
    | `actorUserId` | `string` | Yes | ID of user processing the request |
    | `requestDetails` | `string?` | No | Additional details about the request |
    | `status` | `string?` | No | Status of the request (e.g., "received", "in_progress", "completed", "rejected") |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "dpo", "support_agent") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant data subject request event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.articles15_22.data_subject.request`
    - **GDPR Articles:** Articles 15-22 - Data subject rights
    - **Request Type:** Stored in framework data
    - **Request Details:** Stored in framework data
    - **Status:** Stored in framework data
    - **Risk Level:** Medium

=== "Example"

    **Example usage:**

    ```csharp
    var requestEvent = GdprEvents.DataSubjectRequest(
        dataSubjectId: "user-123",
        requestType: "access",
        actorUserId: "dpo-456",
        requestDetails: "Request for copy of all personal data",
        status: "received",
        sessionId: "session789",
        actorRole: "data_protection_officer"
    );

    await _auditLedger.LogEventAsync(requestEvent);
    ```

---

## DataBreach

Creates a data breach notification event for GDPR Article 33 compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent DataBreach(
        string breachId,
        string actorUserId,
        string breachType,
        string severity,
        int? affectedDataSubjects = null,
        string? description = null,
        string? notificationStatus = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `breachId` | `string` | Yes | Unique identifier for the breach |
    | `actorUserId` | `string` | Yes | ID of user reporting the breach |
    | `breachType` | `string` | Yes | Type of breach (e.g., "unauthorized_access", "data_loss", "system_compromise") |
    | `severity` | `string` | Yes | Severity level (e.g., "low", "medium", "high", "critical") |
    | `affectedDataSubjects` | `int?` | No | Number of affected data subjects |
    | `description` | `string?` | No | Description of the breach |
    | `notificationStatus` | `string?` | No | Notification status (e.g., "detected", "reported_to_authority", "notified_subjects") |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "security_officer", "dpo") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant data breach event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article33.data_breach.occurred`
    - **GDPR Article:** Article 33 - Notification of a personal data breach to the supervisory authority
    - **Breach Type:** Stored in framework data
    - **Severity:** Stored in framework data
    - **Affected Data Subjects:** Stored in framework data
    - **Notification Status:** Stored in framework data
    - **Risk Level:** High

=== "Example"

    **Example usage:**

    ```csharp
    var breachEvent = GdprEvents.DataBreach(
        breachId: "breach-2024-001",
        actorUserId: "security-admin",
        breachType: "unauthorized_access",
        severity: "high",
        affectedDataSubjects: 150,
        description: "Unauthorized access to customer database",
        notificationStatus: "reported_to_authority",
        actorRole: "security_officer"
    );

    await _auditLedger.LogEventAsync(breachEvent);
    ```

---

## DataErased

Creates a data erasure event for GDPR Article 17 compliance (Right to be forgotten).

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent DataErased(
        string dataSubjectId,
        string actorUserId,
        string? erasureReason = null,
        string? dataCategories = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject whose data is being erased |
    | `actorUserId` | `string` | Yes | ID of user performing the erasure |
    | `erasureReason` | `string?` | No | Reason for erasure (e.g., "data_subject_request", "retention_period_expired", "consent_withdrawn") |
    | `dataCategories` | `string?` | No | Categories of data being erased (comma-separated) |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "dpo", "admin") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant data erasure event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article17.data.erased`
    - **GDPR Article:** Article 17 - Right to erasure ("right to be forgotten")
    - **Erasure Reason:** Stored in framework data
    - **Data Categories:** Stored in framework data
    - **Risk Level:** Medium

=== "Example"

    **Example usage:**

    ```csharp
    var eraseEvent = GdprEvents.DataErased(
        dataSubjectId: "user-123",
        actorUserId: "dpo-456",
        erasureReason: "data_subject_request",
        dataCategories: "contact_information,profile_data,preferences",
        sessionId: "session789",
        actorRole: "data_protection_officer"
    );

    await _auditLedger.LogEventAsync(eraseEvent);
    ```

---

## DataExported

Creates a data export event for GDPR Article 20 compliance (Right to data portability).

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent DataExported(
        string dataSubjectId,
        string actorUserId,
        string exportFormat,
        string? dataCategories = null,
        string? destination = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject whose data is being exported |
    | `actorUserId` | `string` | Yes | ID of user performing the export |
    | `exportFormat` | `string` | Yes | Format of exported data (e.g., "json", "csv", "xml") |
    | `dataCategories` | `string?` | No | Categories of data being exported (comma-separated) |
    | `destination` | `string?` | No | Destination or method of export (e.g., "email", "download", "api") |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "dpo", "support_agent") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant data export event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article20.data.exported`
    - **GDPR Article:** Article 20 - Right to data portability
    - **Export Format:** Stored in framework data
    - **Data Categories:** Stored in framework data
    - **Destination:** Stored in framework data
    - **Risk Level:** Low

=== "Example"

    **Example usage:**

    ```csharp
    var exportEvent = GdprEvents.DataExported(
        dataSubjectId: "user-123",
        actorUserId: "support-456",
        exportFormat: "json",
        dataCategories: "contact_information,profile_data,activity_history",
        destination: "email",
        sessionId: "session789",
        actorRole: "customer_support_agent"
    );

    await _auditLedger.LogEventAsync(exportEvent);
    ```

---

## ProcessingRestricted

Creates a processing restriction event for GDPR Article 18 compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent ProcessingRestricted(
        string dataSubjectId,
        string actorUserId,
        string? restrictionReason = null,
        string? dataCategories = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject |
    | `actorUserId` | `string` | Yes | ID of user applying the restriction |
    | `restrictionReason` | `string?` | No | Reason for restriction (e.g., "data_subject_request", "dispute_accuracy", "unlawful_processing") |
    | `dataCategories` | `string?` | No | Categories of data being restricted |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "dpo", "admin") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant processing restriction event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article18.processing.restricted`
    - **GDPR Article:** Article 18 - Right to restriction of processing
    - **Restriction Reason:** Stored in framework data
    - **Data Categories:** Stored in framework data
    - **Risk Level:** Medium

=== "Example"

    **Example usage:**

    ```csharp
    var restrictEvent = GdprEvents.ProcessingRestricted(
        dataSubjectId: "user-123",
        actorUserId: "dpo-456",
        restrictionReason: "data_subject_request",
        dataCategories: "marketing_data,analytics_data",
        sessionId: "session789",
        actorRole: "data_protection_officer"
    );

    await _auditLedger.LogEventAsync(restrictEvent);
    ```

---

## DataRectified

Creates a data rectification event for GDPR Article 16 compliance.

=== "Signature"

    **Method signature:**

    ```csharp
    public static AuditEvent DataRectified(
        string dataSubjectId,
        string actorUserId,
        string? dataField = null,
        string? oldValue = null,
        string? newValue = null,
        string? rectificationReason = null,
        string? sessionId = null,
        string? ipAddress = null,
        string? actorRole = null
    )
    ```

=== "Parameters"

    | Parameter | Type | Required | Description |
    |-----------|------|----------|-------------|
    | `dataSubjectId` | `string` | Yes | Identifier of the data subject |
    | `actorUserId` | `string` | Yes | ID of user performing the rectification |
    | `dataField` | `string?` | No | Field or category of data being rectified |
    | `oldValue` | `string?` | No | Previous value (if applicable) |
    | `newValue` | `string?` | No | New corrected value |
    | `rectificationReason` | `string?` | No | Reason for rectification (e.g., "data_subject_request", "error_correction") |
    | `sessionId` | `string?` | No | Session identifier |
    | `ipAddress` | `string?` | No | IP address of actor |
    | `actorRole` | `string?` | No | Role of actor (e.g., "dpo", "support_agent") |

=== "Returns"

    | Type | Description |
    |------|-------------|
    | `AuditEvent` | GDPR compliant data rectification event |

    **Event Details:**

    - **Event Type:** `io.auditledger.gdpr.article16.data.rectified`
    - **GDPR Article:** Article 16 - Right to rectification
    - **Data Field:** Stored in framework data
    - **Old Value:** Stored in framework data
    - **New Value:** Stored in framework data
    - **Rectification Reason:** Stored in framework data
    - **Risk Level:** Low

=== "Example"

    **Example usage:**

    ```csharp
    var rectifyEvent = GdprEvents.DataRectified(
        dataSubjectId: "user-123",
        actorUserId: "support-456",
        dataField: "email_address",
        oldValue: "old@example.com",
        newValue: "new@example.com",
        rectificationReason: "data_subject_request",
        sessionId: "session789",
        actorRole: "customer_support_agent"
    );

    await _auditLedger.LogEventAsync(rectifyEvent);
    ```

---

## Next Steps

- **[SOC 2 Events](soc2-events.md)** - SOC 2 Framework Helper reference
- **[HIPAA Events](hipaa-events.md)** - HIPAA Framework Helper reference
- **[PCI DSS Events](pcidss-events.md)** - PCI DSS Framework Helper reference
- **[API Overview](overview.md)** - Complete API reference
- **[Quick Start](../getting-started/quick-start.md)** - Get started in 5 minutes

