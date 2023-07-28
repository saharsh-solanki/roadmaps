
## Database
<b>Table of content</b>
<ol>
    <li>
    Learn and understand ACID Properties
        <ul>
            <li>
            Introduction to ACID
            </li>
            <li>
            <details>
            <summary>What is Transaction</summary>
            <p></br>
            In simple terms, a transaction in a database is like a "package deal" that groups together multiple actions or changes you want to make to the data. It's like a single task that is either completes fully or doesn't happen at all.</br></br>
            a transaction is a way to bundle related actions together and ensure they either all succeed or none of them take effect, helping to keep the data accurate and reliable.</br></br>
            For example, let's say you want to transfer money from one bank account to another. In a transaction, you would specify the withdrawal from the source account and the deposit into the destination account as a single unit of work. This ensures that either both actions occur successfully, or none of them happen. If, for some reason, the deposit fails after the withdrawal has already taken place, the transaction will be rolled back, and the money will be returned to the source account.</br></br>
            Transactions help maintain the accuracy and reliability of the database by guaranteeing that changes are applied consistently. They ensure that all the steps within the transaction are treated as a single, indivisible operation. If any part of the transaction fails, the database is restored to its original state, so you don't end up with incomplete or inconsistent changes.</br>
            </p>
            </details>
            </li>
            <li>
            <details>
            <summary>
            Atomicity
            </summary>
            <p></br>
            Atomicity is one of the fundamental properties of a transaction in a database system. It ensures that a transaction is treated as an indivisible, all-or-nothing unit of work. In other words, atomicity guarantees that either all the operations within a transaction are successfully completed, or none of them are applied to the database.</br></br>
            Atomicity ensures that if any part of the transaction fails, for example, due to an error, constraint violation, or system failure, the entire transaction is rolled back, and the database is restored to its state before the transaction started. This rollback mechanism ensures that the database remains in a consistent state and that incomplete or erroneous changes are not persisted.</br></br>
            The concept of atomicity, in the context of transactions, is designed to ensure that it cannot be broken. Atomicity guarantees that either all operations within a transaction are successfully completed and permanently applied, or if any operation fails, the entire transaction is rolled back, and none of the changes made by that transaction are applied to the database.</br></br>
            </p>
            </details>
            </li>
            <li>
            <details>
            <summary>Isolation</summary>
            <p>
            <ul><li>
            <details>
            <summary>Dirty Read </summary><p>
            Suppose there is                                            a trasaction when is in running state TXN1--> there 3 query being running in this transaction. First it selected sales and then again  it selected the SUM of sales now there are two query being executing. But There is another trasection which occured which modified the data and then you run the second query inside the of SUM you get diffrent data. There are 2 Product and price is 100 so total will be 200 now you run the first query of TXN1 you get 2 prduct you added in your report then your second query of TXN1 you are fetching total SUM which is 200 but in between another transaction TXN2 occured and which modified the product to 3 now the total SUM will be 300 in your TXN1 but you have 2 product but you rolled back the TXN2 so your report will be DIRTY means you have 2 product but the total is 300.</br></br>
            example :  A Dirty Read occurs when one transaction reads data that has been modified by another ongoing transaction and has not yet been committed. In your example, TXN1 started with two queries: one to select sales and then another to calculate the SUM of sales, resulting in a total of 200. While TXN1 was still running, another transaction TXN2 modified the product data, changing the number of products from 2 to 3.</br></br>
            Now, when TXN1's second query executes and calculates the SUM of sales, it reads the modified data from TXN2, leading to a total of 300. However, TXN2 is still in progress and has not been committed yet. Due to the Dirty Read, TXN1 has "dirty" or inconsistent data, as it sees 2 products but a total that indicates 3 products were involved.</br></br>
            In database systems, transactions are expected to provide isolation from one another, so that the changes made by one transaction are not visible to other transactions until the changes are committed. Dirty Reads can occur in transaction isolation levels that allow them, such as the "Read Uncommitted" isolation level.
            </p>
            </details>
            </li></ul>
            </p>
            </details>
            </li>
            <li>
            Consistency
            </li>
            <li>
            Durability
            </li>
            <li>
            ACID Practical Example
            </li>
            <li>
            Phantom Reads
            </li>
            <li>
            Serializable vs repeatable reads 
            </li>
            <li>
            Eventual Consistency 
            </li>
            <li>
            ACID Quiz 
            </li>
        </ul>
    </li>
</ol>



