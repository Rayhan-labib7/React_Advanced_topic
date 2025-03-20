// hooks
import { useEffect, useState } from "react";

export const useDebounce = (value, delay=500) => {
    const [debouncedValue, setDebouncedValue] = useState(value);
    useEffect(() => {
        const handler = setTimeout(() => {
            setDebouncedValue(value);
        }, delay);
        return () => {
            clearTimeout(handler);
        };
    }, [value, delay]);

    return debouncedValue;

//
import React, { useState, useEffect } from "react";
import { useDebounce } from './hooks';

const PaginationExample = () => {
  const [page, setPage] = useState(1);
  const [pageSize] = useState(5);

  const [total, setTotal] = useState(0);
  const [loading, setLoading] = useState(false);

  const [search,setSearch] = useState("");
  const debouncedSearch = useDebounce(search);
  const [data, setData] = useState([]);
  // Fake data - Simulate a fake API
  const countryData = [
    { id: 1, name: "Bangladesh" },
    { id: 2, name: "India" },
    { id: 3, name: "Canada" },
    { id: 4, name: "USA" },
    { id: 5, name: "UK" },
    { id: 6, name: "Australia" },
    { id: 7, name: "Pakistan" },
    { id: 8, name: "Sri Lanka" },
    { id: 9, name: "Nepal" },
    { id: 10, name: "Bhutan" },
    { id: 11, name: "Japan" },
    { id: 12, name: "China" },
  ];

  // Fake API call to filter data by search and paginate
  const fetchData = () => {
    setLoading(true);
    console.log("api call")
    const filteredData = countryData.filter((item) =>
      item.name.toLowerCase().includes(debouncedSearch.toLowerCase())
    );
    const startIndex = (page - 1) * pageSize;
    const paginatedData = filteredData.slice(startIndex, startIndex + pageSize);
    setData(paginatedData);
    setTotal(filteredData.length);

    setLoading(false);
  };

  useEffect(() => {
    fetchData();
  }, [page, debouncedSearch]); // Re-fetch data when page or searchTerm changes
//   console.log("serch",search)
  return (
    <div>
      <h2>Paginated & Searchable Data (Fake API)</h2>

      {/* Search Input */}
      <input
        type="text"
        placeholder="Search country..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
      />

      {/* List of Countries */}
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.length > 0 ? (
            data.map((item) => <li key={item.id}>{item.name}</li>)
          ) : (
            <li>No results found</li>
          )}
        </ul>
      )}

      {/* Pagination Controls */}
      <button disabled={page === 1} onClick={() => setPage(page - 1)}>
        Prev
      </button>
      <button disabled={page * pageSize >= total} onClick={() => setPage(page + 1)}>
        Next
      </button>

      <p>Page {page} of {Math.ceil(total / pageSize)}</p>
    </div>
  );
};

export default PaginationExample;
